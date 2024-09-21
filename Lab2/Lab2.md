
**IaaS Deployment Architecture**!
Internet- It represents the external access for users to interact with the application.

Load Balancer-It distributes the incoming traffic across multiple web servers.

Web Server- A VM running Flask app, responsible for handling HTTP Requests.

Postgres DB-A VM running this manages the application data.

**PaaS Deployment Architecture**

Internet- It represents the external access for users to interact with the application.

Load Balancer- Distributes the incoming traffic among multiple servers.

Web Server-Hosted on a PaaS platform that abstracts away the underlying infrastructure, allowing developers to focus on the application code.

Postgres DB-A VM running this manages the application data.

**On-Premises Deployment Architecture**

Internet- It represents the external access for users to interact with the application.

Load Balancer- Distributes the incoming traffic among multiple servers.

Web Server-Hosted on a PaaS platform that abstracts away the underlying infrastructure, allowing developers to focus on the application code.

Postgres DB-An on-premises database server that manages application data, requiring regular maintenance, backups, and scaling considerations.
