# Deploy ELK Stack using Ansible

## Before you run the ansible scripts
1) Make sure the variables set in ./group_vars are correctly defined.
2) Sensitive variables below have to exist as environment variables within the shell running the script.
   (You can create a .bashrc file and do a `source .bashrc` in your cloned repo and export these variables first.)
   1) DOCKER_PW
   2) DOCKER_USER
   3) DOCKER_URL



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


# For Filebeat
## To build filebeat docker images and push to repo
`ansible-playbook build-image.yml -t build-fb -i ./hosts -u <user>`

## To deploy filebeat to DEV CI QA servers
`ansible-playbook deploy.yml -t deploy-fb -i ./hosts -u <user>`

## To update filebeat to DEV CI QA servers
`ansible-playbook deploy.yml -t update-fb-conf -i ./hosts -u <user>`

# For 2-Node Elasticsearch in ELK
## To build ELK docker images and push to repo
`ansible-playbook build-image.yml -t build-elk -i ./hosts -u <user>`

## To deploy ELK containers to logging server
`ansible-playbook deploy.yml -t deploy-elk -i ./hosts -u <user>`

## To update ELK configuration files to logging server
`ansible-playbook deploy.yml -t update-elk-conf -i ./hosts -u <user>`

## To setup ELK curators config files to logging server
`ansible-playbook deploy.yml -t setup-curator -i ./hosts -u <user>`

## To update ELK curators config files to logging server
`ansible-playbook deploy.yml -t update-curator -i ./hosts -u <user>`
