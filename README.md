# Deploy and Configure Java Boilerplate Application

This Ansible playbook sets up a Java boilerplate application on a fresh Ubuntu 22.04 server. It installs the necessary packages, configures PostgreSQL and RabbitMQ, deploys the Java application, and sets up Nginx as a reverse proxy.

## Prerequisites

- Ansible installed on your local machine.
- A fresh Ubuntu 22.04 server with SSH access.
- User with sudo privileges.

## Playbook Details

- Playbook Name: Deploy and configure Java boilerplate application
- Host: hng
- User: hng (created during playbook execution)
- Database User: admin
- Database Name: stage_5b_db
- Database Password: password
- Java Version: OpenJDK 17
- Maven Version: Latest available in Ubuntu repository
- Nginx Version: 1.26.*

## Installation
1. Clone the Repository:
```bash
git clone https://github.com/hngprojects/hng_boilerplate_java_web.git -b devops /opt/stage_5b
```
2. Update the Ansible Inventory:
Add your server details to the Ansible inventory file.

3. Run the Playbook:
```bash
ansible-playbook -i inventory.cfg playbook.yaml
```

## Tasks Overview
1. **System Update and Package Installation**:
- Updates the apt cache.
- Installs required packages including Git, OpenJDK, Maven, PostgreSQL, RabbitMQ, and Nginx.

2. **User Setup**:
- Creates a user hng with sudo privileges.
  
3. **Repository Setup**:
- Clones the Java boilerplate application repository.

 4. **Database Configuration**:
- Sets up PostgreSQL with a new user and database.
- Saves PostgreSQL credentials securely.

5. **Environment Configuration**:
- Sets up environment variables in the .env file.
- Updates the pom.xml file with Spring Boot dependencies.

6. **RabbitMQ Configuration**:
- Starts and enables RabbitMQ.

7. **Application Build and Deployment**:
- Resolves Maven dependencies.
- Builds the Java application.
- Sets up a systemd service for the application.

8. **Nginx Configuration**:
- Installs and configures Nginx as a reverse proxy.
- Enables the site and removes the default configuration.

9. **Logging Configuration**:
- Sets up logging for the application.
- Configures log rotation for the application's logs.

### Handlers
- **Restart Application Service**:
  Restarts the Java application service.
- **Reload Nginx**:
  Reloads Nginx to apply the new configuration.

3. Run the playbook using the command:
```bash
ansible-playbook -i inventory.cfg main.yaml
```
