
# ContentSphere – Infrastructure Automation Using Ansible

## 1. Project Overview

ContentSphere is an infrastructure automation project that uses Ansible
to configure a Linux web server and deploy a sample web application.
The project demonstrates configuration management, automation,
reusable roles, Jinja2 templates, and idempotent deployments.

## 2. Objectives

- Automate Nginx installation and configuration.
- Configure a managed Ubuntu server using Ansible.
- Deploy a dynamic HTML webpage using a Jinja2 template.
- Manage services and configuration files automatically.
- Validate successful deployment and idempotency.

## 3. Architecture

Control Node:
- Ubuntu
- Ansible Core
- Inventory and playbooks
- SSH connectivity to the Managed Node

Managed Node:
- Ubuntu
- Nginx web server
- ContentSphere webpage
- Application directory: /var/www/contentsphere

Deployment flow:

Control Node → SSH → Managed Node → Install and Configure Nginx
→ Deploy ContentSphere HTML → Verify HTTP Response

## 4. Technologies Used

- Ansible
- Ubuntu Linux
- Nginx
- YAML
- Jinja2
- SSH
- HTML and CSS

## 5. Project Structure

ContentSphere-Ansible-Project/
├── ansible.cfg
├── inventory
├── group_vars/
│   └── webserver.yml
├── playbooks/
│   └── server-setup.yml
├── roles/
│   └── webserver/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       └── templates/
│           ├── index.html.j2
│           └── nginx-site.conf.j2
├── screenshots/
├── documentation/
└── README.md

## 6. Deployment Commands

Check managed-host connectivity:

ansible webserver -m ansible.builtin.ping

Validate playbook syntax:

ansible-playbook playbooks/server-setup.yml --syntax-check

Deploy the application:

ansible-playbook playbooks/server-setup.yml

Verify HTTP response:

ansible webserver -b -m ansible.builtin.command -a "curl -I http://127.0.0.1"

## 7. Validation Results

- Ansible connectivity: Successful
- Nginx installation: Successful
- ContentSphere webpage deployment: Successful
- HTTP response: 200 OK
- Second deployment: changed=0
- Failed tasks: 0

The second playbook execution confirmed idempotency: the system
was already in the desired state, so no changes were required.

## 8. Conclusion

The project demonstrates how Ansible automates web-server configuration
and application deployment on a remote Ubuntu host. Reusable roles,
variables, templates, handlers, and idempotent tasks improve
consistency and reduce manual administration.
