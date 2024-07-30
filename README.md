# Deploy and Configure Java Boilerplate Application

## Overview
This Ansible playbook automates the deployment and configuration of a Java boilerplate application. It sets up the environment, installs necessary software, configures PostgreSQL and RabbitMQ, builds the Java application, and sets up Nginx as a reverse proxy.

## Requirements
• Ansible installed on the control machine.
• Target host running Ubuntu.
• Access to the target host with sudo privileges.

## Variables
• db_user: PostgreSQL database user (default: "admin").
• db_name: PostgreSQL database name (default: "stage_5b_db").
• db_password: PostgreSQL database password (generated randomly).

## Playbook Breakdown
1. Update apt Cache
Updates the package index to ensure the latest versions of packages.

2. Install Required Packages
Installs the following packages:

• git
• openjdk-17-jdk
• maven
• postgresql
• postgresql-contrib
• python3-psycopg2
• rabbitmq-server
• nginx

3. Create User
Creates a user named hng with sudo privileges.

4. Ensure Directory Exists
Creates the /opt/stage_5b directory with appropriate permissions.

5. Clone Repository
Clones the Java boilerplate repository from GitHub into the /opt/stage_5b directory.

6. Configure PostgreSQL
Creates a PostgreSQL user and database with the provided credentials.

8. Save PostgreSQL Credentials
Stores PostgreSQL credentials in /var/secrets/pg_pw.txt.

9. Ensure Environment Variables are Set
Adds necessary environment variables to /opt/stage_5b/.env.

10. Configure RabbitMQ
Ensures RabbitMQ is started and enabled.

11. Create application.properties
Creates the application.properties file for the Java application with database and RabbitMQ configurations.

12. Build Java Application
Builds the Java application using Maven.

13. Create Systemd Service File
Creates a systemd service file to manage the Java application.

14. Start and Enable Application Service
Starts and enables the Java application service.

15. Add Nginx Signing Key and Repository
Adds the Nginx signing key and repository to the system.

16. Install Nginx
Installs the specified version of Nginx.

17. Configure Nginx Reverse Proxy
Sets up Nginx as a reverse proxy for the Java application.

18. Enable Nginx Site
Enables the Nginx site configuration and removes the default configuration.

19. Create Log Directory
Creates a directory for application logs.

20. Set Up Logging in .env
Configures logging paths in the .env file.

21. Configure Log Rotation
Sets up log rotation for application logs.

## Handlers
Reload Nginx: Reloads Nginx configuration when changes are made.

## Usage
1. Ensure you have Ansible installed on your control machine.

2. Update the hosts file or inventory with your target host.

3. Run the playbook using the command:
```bash
ansible-playbook -i inventory.cfg main.yaml
```
