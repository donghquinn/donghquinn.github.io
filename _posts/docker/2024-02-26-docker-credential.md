---
title: 개인 도커 이미지 허브와 크레덴셜
author: donghquinn
date: 2024-02-26 06:13:00 +0900
categories: [Docker, Credential]
tags: [docker, docker-compose, credential]
comments: true
math: true
mermaid: true
# image:
#   path: assets/img/docker.png
#   alt: Docker
---

<img data-action="zoom" src="/assets/img/docker.png" alt="Docker Logo"/>

## 도커 이미지 허브

도커 이미지는 빌드되어 정적인 상태로 관리된다. 때문에 저장장치에 이미지를 업로드하여 url을 통해 내려 받아 와 사용할 수 있다. 이른바 CI/CD 의 일종으로 볼 수 있을 것 같다. 그런데 개인적인 프로젝트나, 회사 내부 프로젝트일 경우 이미지는 내부에서 관리되어야 하고 유출되면 곤란하다. 때문에 도커 이미지 레지스트리 관리 오픈소스 툴인 harbor 를 이용해 이미지를 관리해 왔다.

## 보안

이미지를 업로드한 저장소에 접근하기 위해선 저장소 접근 권한을 통해 로그인을 해야 한다. 그런데 리눅스 기반의 운영체제에서 (다른 운영체제는 잘 모르겠다) docker login 명령어를 통해 접근하려고 하면, 로컬에 해당 민감정보가 저장되어 버린다는 끔찍한 문제점이 존재한다. 때문에 도커에서도 공식적으로 이러한 방식이 아닌 credential을 이용해 접근하라고 권고하고 있다.

## Docker Credential

- [공식 레포지토리](https://github.com/docker/docker-credential-helpers
)

Credential은 로컬에 그대로 저장하는 것이 아닌, 암호화 시키고 사용할 때 인증을 해서 접근 권한을 가져와 사용할 수 있게 해 준다. 어떤 능력자 분이 설치하는 스크립트를 공유해 주셔서 이를 공유해본다.

- [스크립트 원문](https://geoffhudik.com/tech/2020/09/15/docker-pass-credential-helper-on-ubuntu/)

```shell
#!/bin/sh
# Sets up a docker credential helper so docker login credentials are not stored encoded in base64 plain text.
# Uses the pass secret service as the credentials store.
#
# If previously logged in w/o cred helper, docker logout <registry> under each user or remove ~/.docker/config.json.
#
# For Swarm use just run once on a manager.
# Script written for use on Ubuntu.
# Run elevated logged in as the target user.
# To remove cred helper:
#   - delete /usr/local/bin/docker-credential-pass
#   - remove '{ "credsStore": "pass" }' from ~/.docker/config.json
# Ensure executable in git:
# git update-index --chmod=+x path/docker-credentials.sh
if ! [ $(id -u) = 0 ]; then
   echo "This script must be run as root"
   exit 1
fi
# Install dependencies - jq more optional for existing varying configuration in ~/.docker/config.json.
apt update && apt-get -y install gnupg2 pass rng-tools jq
# Check for later releases at https://github.com/docker/docker-credential-helpers/releases
version="v0.6.3"
archive="docker-credential-pass-$version-amd64.tar.gz"
url="https://github.com/docker/docker-credential-helpers/releases/download/$version/$archive"
# Download cred helper, unpack, make executable, move it where it'll be found
wget $url \
    && tar -xf $archive \
    && chmod +x docker-credential-pass \
    && mv -f docker-credential-pass /usr/local/bin/
# Done with the archive
rm -f $archive
config_path=~/.docker
config_filename=$config_path/config.json
# Could assume config.json isn't there or overwrite regardless and not use jq (or sed etc.)
# echo '{ "credsStore": "pass" }' > $config_filename
if [ ! -f $config_filename ]
then
    if [ ! -d $config_path ]
    then
        mkdir -p $config_path
    fi
    # Create default docker config file if it doesn't exist (never logged in etc.). Empty is fine currently.
    cat > $config_filename <<EOL
{
}
EOL
    echo "$config_filename created with defaults"
else
    echo "$config_filename already exists"
fi
# Whether config is new or existing, read into variable for easier file redirection (cat > truncate timing)
config_json=`cat $config_filename`
if [ -z "$config_json" ]; then
    # Empty file will prevent jq from working
    $config_json="{}"
fi
# Update Docker config to set the credential store. Used sed before but messy / edge cases.
echo "$config_json" | jq --arg credsStore pass '. + {credsStore: $credsStore}' > $config_filename
# Output / verify contents
echo "$config_filename:"
cat $config_filename | jq
# Help with entropy to prevent gpg2 full key generation hang
# Feeds data from a random number generator to the kernel's random number entropy pool
rngd -r /dev/urandom
# To cleanup extras from multiple runs: gpg --delete-secret-key <key-id>; gpg --delete-key <key-id>
echo "Generating GPG key, accept defaults but consider key size to 2048, supply user info"
gpg2 --full-generate-key
echo "Adjusting permissions"
sudo chown -R $USER:$USER ~/.gnupg
sudo find ~/.gnupg -type d -exec chmod 700 {} \;
sudo find ~/.gnupg -type f -exec chmod 600 {} \;
# List keys
gpg2 -k
# Grab target key
key=$(gpg2 --list-secret-keys | grep uid -B 1 | head -n 1 | sed 's/^ *//g')
echo "Initializing pass with key $key"
pass init $key
# Image can't be found when Swarm attempts to pull later if a pass phrase is here.
echo "Do not set a passphrase for this step (*IMPORTANT*)"
pass insert docker-credential-helpers/docker-pass-initialized-check
# Optionally show password but mask ***
# pass show docker-credential-helpers/docker-pass-initialized-check | sed -e 's/\(.\)/\*/g'
echo "Docker credential password list (empty initially):"
docker-credential-pass list
echo "Done. Ready to test. Run: docker login <registry>"
echo "After login run: docker-credential-pass list; cat ~/.docker/config.json; pass show"
```

### 도메인 등록

도커 로그인을 진행해서 도메인을 등록한다.

```shell 
sudo docker login <docker hub | registry address>
>>username:
>>password:
>> succeed
```

### 리스트 업

```shell
sudo docker-credential-pass list
>> {"example.com":"username"}
```

### 활성화

아래 명령어를 입력하면 위에서 인증 키를 생성할 때 입력한 패스워드를 입력할 수 있는 창이 뜰 것이다. 이후에 저장소에 접근하면 정상적으로 가능해진다.

```shell
sudo pass ls docker-credential-helpers/docker-pass-initialized-check
```
