# Ansible Advanced Homework Assignment

## Pre-requisites

1. From OPENTLC Service Catalogs, order:
   1. Ansible Tower Lab
   2. OpenStack for Ansible
2. Configure HA Ansible Tower.
3. Create a github.com account to pull Ansible projects from.


## Tower Workflow

Run the "Deploy 3-Tier Workflow" from [Ansible Tower](https://tower1.28dc.example.opentlc.com/).

This workflow performs the following steps:

1. Does a Project Sync of the project (Homework).
2. Deploy Production (AWS) environment
   1. Provision AWS instances (Provision_AWS.yml).
   2. AWS 3-tier inventory (Configure_3TA_AWS.yml).
   3. Add AWS SSH key to Tower (add_aws_key.yml).
3. Deploy Development (OSP) environment.
   1. Provision OSP instances (Provision_OSP.yml).
   2. Configure 3 Tier OSP application (Configure_3TA_OSP.yml).
   3. Run smoke test (smoke-test.yml).
4. Upon successful deployment of the development environment (as tested by the smoke test), deploy the production 3-tier application to AWS.
   1. Run an inventory sync of the AWS inventory.
   2. Configure 3 Tier AWS application (Configure_3TA_AWS.yml).
   3. Run smoke test (smoke-test-aws.yml).
5. Delete OSP instances if development (OSP) environment was unsuccessful (cleanup_OSP.yml).

## Playbooks and roles
### Playbooks
* Provision_AWS.yml
* add_aws_key.yml
* Provision_OSP.yml
* Check_AWS_instances.yml
* Configure_3TA_AWS.yml
* Configure_3TA_OSP.yml
* cleanup_OSP.yml
* smoke-test-aws.yml
* smoke-test.yml

### Roles
* haproxy
  Installs and configures haproxy.
* osp-del-instances
  Deletes OSP instances.
* osp-facts
  Creates dynamic inventory for OSP.
* postgres
  Installs Postgres.
* repos
  Deploys a yum repo config file that is encrypted with ansible-vault.
* tomcat
  Installs Tomcat.
