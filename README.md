# Container checkpackages

Tool for validating packages installed in a docker image

Supports Ubuntu, debian, centos and alpine

## Build 
    go build 

with docker 

    docker build -t checkpackages . 

## Usage
checkpackages check installed packages in the docker images and compares it to the policy file

returns 1 if unauthorized packages found, 0 otherwise


    checkpackages [IMAGE] [POLICY-FILE]

with docker

    docker run --rm -v /var/run/docker.sock:/var/run/docker.sock -v [POLICY_PATH]:/tmp/policy checkpackages [IMAGE] /tmp/policy

## Policy file
One package per line

to exlude a patern, use prefix !


Example:

    apache2
    !libapache2-mod-apparmor

will fail on apache2, but not on libapache2-mod-apparmor

## Test
    docker build -t checkpackages . 
    cd test
    sh test_all.sh


