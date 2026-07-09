
# RoboShop Ansible — Configuration Management
 
Ansible playbooks to configure and deploy all RoboShop
microservices on EC2 instances. Automates the complete
application stack setup including databases, message queues,
and all backend services.
 
---
 
## What This Repo Covers
 
| Service | Playbook | Type |
|---------|----------|------|
| Frontend (Nginx) | `frontend.yaml` | Web server |
| Catalogue | `catalogue.yaml` | Node.js microservice |
| User | `user.yaml` | Node.js microservice |
| Cart | `cart.yaml` | Node.js microservice |
| Shipping | `shipping.yaml` | Java microservice |
| Payment | `payment.yaml` | Python microservice |
| MongoDB | `mongodb.yaml` | Database |
| MySQL | `mysql.yaml` | Database |
| Redis | `redis.yaml` | Cache |
| RabbitMQ | `rabbitmq.yaml` | Message queue |
| All services | `roboshop.yaml` | Master playbook |
 
---
 
## Structure
 
```
roboshop-ansible/
├── roboshop.yaml       # master playbook — runs all services
├── catalogue.yaml      # catalogue service setup
├── cart.yaml           # cart service setup
├── user.yaml           # user service setup
├── payment.yaml        # payment service setup
├── shipping.yaml       # shipping service setup
├── frontend.yaml       # nginx frontend setup
├── mongodb.yaml        # MongoDB database setup
├── mysql.yaml          # MySQL database setup
├── redis.yaml          # Redis cache setup
├── rabbitmq.yaml       # RabbitMQ message queue setup
├── vars.yaml           # shared variables
├── inventory.ini       # hosts inventory
├── nginx.conf          # Nginx configuration
└── *.service           # systemd service files per component
```
 
---
 
## How to Run
 
```bash
# Clone the repo
git clone https://github.com/mamatha-ravi/roboshop-ansible
 
# Test connectivity to all hosts
ansible all -m ping -i inventory.ini
 
# Run specific service playbook
ansible-playbook -i inventory.ini catalogue.yaml
 
# Run all services with master playbook
ansible-playbook -i inventory.ini roboshop.yaml
 
# Dry run — see what will change
ansible-playbook -i inventory.ini roboshop.yaml --check
```
 
---
 
## Inventory
 
```ini
[catalogue]
<catalogue-ip> ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/key.pem
 
[mongodb]
<mongodb-ip> ansible_user=ec2-user ansible_ssh_private_key_file=~/.ssh/key.pem
 
# ... all services defined here
```
 
---
 
## What Each Playbook Does
 
Each service playbook:
1. Installs required packages (Node.js, Java, Python, etc.)
2. Creates application user
3. Downloads and extracts application artifact
4. Configures systemd service file
5. Starts and enables the service
6. Loads data if required (MongoDB, MySQL)
 
---
 
## Tech Stack
 
Ansible · AWS EC2 · Node.js · Java · Python · MongoDB · MySQL ·
Redis · RabbitMQ · Nginx · systemd · Linux (RHEL)
 
---
 
## Related Repos
 
| Repo | Description |
|------|-------------|
| [roboshop-infra-dev](https://github.com/mamatha-ravi/roboshop-infra-dev) | Terraform infrastructure for these EC2 instances |
| [terraform-aws-eks](https://github.com/mamatha-ravi/terraform-aws-eks) | Kubernetes version of the same project |
 
---
 
## Author
 
Mamatha Ravipati
📍 Hyderabad, India
📧 mamata.r@gmail.com
🔗 [github.com/mamatha-ravi](https://github.com/mamatha-ravi)
