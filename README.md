# haufe-test

## What this projects does
This project is a test submitted by Hauge/Umantis and it makes use of Ansible to:
- build an ec2 instance
- install docker
- build a docker image based on centos
  - use dockerfile to configure nginx to listen on ports 80/443, with 80->443 redirect and basic authentication
- run the docker container

## Prerequisites

### Install Ansible 2.1 vith virualenv
```shell
pip install --upgrade pip virtualenv virtualenvwrapper
virtualenv ansible2.1
source ansible2.1/bin/activate
pip install ansible==2.1
```
### Set AWS credentials
Ansible expects to find `AWS_ACCESS_KEY` and `AWS_SECRET_ACCESS_KEY AWS_ACCESS_KEY` in your environment (if you don't have any, contact me).

Also the private key `haufe-devops.pem` has to be placed in your `~/.ssh` and it has been sent separately.

Default AWS region is `eu-central-1` set as variable in the playbook.

## AWS config out of this project
A security group

## How to run the test
In the root directory, just run:
`ansible-playbook haufe.yml`
Once Ansible is done, connect with http or https to the IP returned by the ansible output.

http is auto redirected to https, which uses self-signed certificate (so it must be trusted manually).

Username and password for basic auth is: `haufe/haufe`

## Enhancements
- ssl CSR, Key and htpasswd have been pre-generated. They can be provisioned either as part of `RUN` in the dockerfile or with another ansible playbook executed still with the dockerfile.
