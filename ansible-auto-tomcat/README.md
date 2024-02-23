# Ansible automation to configure Tomcat on multi environment

![image](https://github.com/assefadawit73/dawit-devops-proj/assets/66095194/1ef75b94-fb9e-471d-b4df-c496daa782b0)


## TABLE OF CONTENTS

1. [Goal](#goal)
2. [Pre-Requisites](#pre-requisites)
3. [Automation](#automation)
4. [Validation](#validation)
5. [Ansible-Architecture](#ansible-architecture)

## Goal
The goal of this project is to automate Tomcat application server deployment on multi environments – Dev & Prod.

## Pre-Requisites
- Install Ansible control engine on the development platform.
- Install Visual Studio Code on the development platform.
- Deploy Ansible Control Node, Dev Application server & Prod Application Server as per the above architecture.

## Automation
Develop Ansible Role to provision the Tomcat application server on the target environment as per the below configuration:

1. Install common dependencies AWS-CLI, wget, curl, git.
2. Install Java 11.
3. Download and install Tomcat into CATALINA HOME ‘/usr/local/tomcat’.
4. Configure systemd service to manage the ‘tomcat’ service.
5. Configure Tomcat user ‘admin’ and assign manager & admin role access.
6. Integrate Ansible vault to store the Tomcat user ‘admin’ passwords.
7. Restart Apache Tomcat service only when the Tomcat configuration file changes.

## Validation
- Run Ansible Playbook to invoke the Role and configure the Dev environment.
- Run Ansible Playbook to invoke the Role and configure the Prod environment.
- Access the Tomcat page using curl from the Ansible control node.


