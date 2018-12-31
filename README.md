# Deploy ELK Stack using Ansible

## Before you run the ansible scripts
1) Make sure the variables set in ./group_vars are correctly defined.
2) Sensitive variables below have to exist as environment variables within the shell running the script.
   (You can create a .bashrc file in your cloned repo and export these variables first.)
   1) DOCKER_PW
   2) DOCKER_USER
   3) DOCKER_URL
   4) DOCKER_EMAIL - (this is only used if you are building filebeat on centos < 7)

## To edit the filebeat/elk config files
```
# relative to working dir ./roles
...
+-- elk
|   +-- files
|   |   +-- elasticsearch   # edit config files + docker files here
|   |   +-- logstash        # edit config files + docker files here
|   |   +-- kibana          # edit config files + docker files here
...
+-- filebeat      # this is for docker versions > 1.7.1, and docker-compose versions > 1.5.1
|   +-- files     # edit config files + docker files here
...
```


# For ROR Filebeat
## To build filebeat docker images and push to repo
`ansible-playbook build-image.yml -t build-fb -i ./hosts -u deploy`

## To deploy filebeat to DEV, ADAGIO (Centos >= 7) servers
`ansible-playbook deploy.yml -t setup-fb -i ./hosts -u deploy`

## To deploy filebeat to CI, QA (Centos < 7) servers
`ansible-playbook deploy.yml -t setup-fb-old -i ./hosts -u deploy`

# For ELK
## To build ELK docker images and push to repo
`ansible-playbook build-image.yml -t build-elk -i ./hosts -u minion`

## To deploy ELK containers to MINION server
`ansible-playbook deploy.yml -t setup-elk -i ./hosts -u minion`

## To update ELK configuration files to MINION server
`ansible-playbook deploy.yml -t update-elk-conf -i ./hosts -u minion`

## To setup ELK curators config files to MINION server
`ansible-playbook deploy.yml -t setup-curator -i ./hosts -u minion`

## To update ELK curators config files to MINION server
`ansible-playbook deploy.yml -t update-curator -i ./hosts -u minion`
