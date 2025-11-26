🚀 Roboshop 3-Tier Deployment Using Ansible

Automated deployment of the complete Roboshop Application (Frontend + Backend + Databases + Messaging) using Ansible playbooks.

This project includes individual playbooks for each service, service files, config templates, and repo files required to deploy the entire 3-tier architecture.

🏗️ Architecture Overview
Tier 1 – Frontend

Deployed using Nginx

Serves UI

Forwards traffic to backend microservices

Tier 2 – Backend Services

Services automated in this repository:

Service	Technology
catalogue	NodeJS
user	NodeJS
cart	NodeJS
shipping	Java
payment	Python
roboshop	NodeJS main router

Each service includes:

.yaml Ansible playbook

.service systemd file

Necessary config files

Tier 3 – Database + Caching + Messaging
Component	Purpose
MongoDB	Stores product & user data
MySQL	Used by shipping service
Redis	Used for cart sessions
RabbitMQ	Payment queue management
📁 Repository Structure
roboshop-ansible/
├── cart.service
├── cart.yaml
├── catalogue.service
├── catalogue.yaml
├── catalogue_output.yaml
├── frontend.yaml
├── inventory.ini
├── mongo.repo
├── mongodb.yaml
├── mysql.yaml
├── nginx.conf
├── nginx.config
├── payment.service
├── payment.yaml
├── rabbitmq.repo
├── rabbitmq.yaml
├── redis.yaml
├── roboshop.yaml
├── shipping.service
├── shipping.yaml
├── user.service
├── user.yaml
└── README.md

🧩 What This Project Automates

✔ Installing dependencies (NodeJS, Java, Python, Nginx, Databases)
✔ Deploying each microservice
✔ Setting up systemd services
✔ Configuring repositories (MongoDB, RabbitMQ, MySQL)
✔ Downloading and extracting Roboshop app code
✔ Updating config files for each service
✔ Starting & enabling services

📝 Inventory File (inventory.ini)

Example:

[frontend]
frontend.example.com

[backend]
catalogue.example.com
user.example.com
cart.example.com
shipping.example.com
payment.example.com
roboshop.example.com

[databases]
mongodb.example.com
mysql.example.com
redis.example.com
rabbitmq.example.com

🚀 How to Run
Step 1 — Test connection
ansible -i inventory.ini all -m ping

Step 2 — Run any service individually
ansible-playbook -i inventory.ini catalogue.yaml
ansible-playbook -i inventory.ini user.yaml
ansible-playbook -i inventory.ini cart.yaml
ansible-playbook -i inventory.ini shipping.yaml
ansible-playbook -i inventory.ini payment.yaml
ansible-playbook -i inventory.ini redis.yaml
ansible-playbook -i inventory.ini mongodb.yaml
ansible-playbook -i inventory.ini mysql.yaml
ansible-playbook -i inventory.ini rabbitmq.yaml

Step 3 — Deploy full application

(If you want to create a master playbook later)

ansible-playbook -i inventory.ini roboshop.yaml

📷 Architecture Diagram (ASCII)
                   ┌──────────┐
                   │ Frontend │
                   │  Nginx   │
                   └─────┬────┘
                         │
        ┌────────────────┴────────────────┐
        │           Backend               │
        │ Catalogue | User | Cart         │
        │ Shipping  | Payment | Roboshop  │
        └───────┬───────────────┬────────┘
                │               │
                ▼               ▼
        ┌────────────┐   ┌───────────────┐
        │  MongoDB    │   │    MySQL      │
        └────────────┘   └───────────────┘
                │               │
                ▼               ▼
          ┌──────────┐     ┌───────────┐
          │  Redis    │     │ RabbitMQ  │
          └──────────┘     └───────────┘

🎯 Learning Outcomes

Managing multi-service deployments using Ansible

Working with systemd service files

Configuring Nginx for microservices

Automating database setup

Using templates, repos, handlers

Implementing a real-world DevOps deployment scenario
