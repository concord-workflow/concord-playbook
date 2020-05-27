# concord-playbook

A Concord flow and an Ansible playbook to install Concord.

See [notes](#notes) below for compatibility information.

## Prerequisites

- PostgreSQL 10+;
- at least one VM for Server and Agent each.

The Server VM requirements:
- access to the DB host;
- port 8001 open.

## Usage

### Using Concord

Requires Concord 1.48.0 or newer.

- place the private key into the `concord.pem` file in the root directory;
- copy the `inventory.example.ini` into `inventory.ini`. Open the file and set
  the required environment details;
- run on a local Concord instance using the `./run.sh` script.

### Using Ansible CLI

Requires Ansible 2.7 or newer.

- place the private key into the `concord.pem` file in the root directory;
- set the expected permissions:
  ```
  $ chmod 600 concord.pem
  ```
- copy the `inventory.example.ini` into `inventory.ini`. Open the file and set
  the required environment details;
- run:
  ```
  $ ansible-galaxy install -r requirements.yml

  $ export ANSIBLE_HOST_KEY_CHECKING=false
  $ export ANSIBLE_PIPELINING=true
  $ ansible-playbook -u ubuntu --private-key=concord.pem -i inventory.ini playbook.yml
  ```

### Access

Access the UI by logging into http://SERVER_IP:8001/#/login?useApiKey=true
using the API key configured in the inventory file.

## Notes

Tested on AWS using:
- `ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-20200408` AMI
- t2.micro computes
- PostgreSQL 10.12-R1 on RDS
- Concord 1.50.1
