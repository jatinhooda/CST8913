# High-Level Design (HLD) Document

## 1. Solution Diagram
![output (1)](https://github.com/user-attachments/assets/403197e4-b3a3-4e06-b54d-d6da302d2091)


During this migration, we will rehost the 3-tier eCommerce application on AWS by leveraging the following services:

### Frontend:
- The web application will be deployed on EC2 instances.
- An Application Load Balancer (ALB) will be used to distribute incoming traffic evenly across the servers.

### Backend:
- The API will be hosted on EC2 instances within an Auto Scaling group that automatically adjusts the number of instances based on demand.

### Database:
- The SQL database will be moved to Amazon RDS with Multi-AZ deployment to ensure high availability and automatic failover in case of issues.

### DNS Management:
- Amazon Route 53 will be configured to handle DNS routing and offer failover solutions to ensure traffic can be managed across different regions if necessary.

**Summary of Architectural Design:**
- Frontend: EC2 instances behind an ALB to balance the load.
- Backend: EC2 instances in an Auto Scaling Group to manage traffic dynamically.
- Database: Amazon RDS with Multi-AZ for high availability and failover support.

## 2. Major AWS Services and Their Roles

- **Amazon EC2:** 
  - Used to host both the frontend web application and backend API.
  - EC2 allows flexible scaling to accommodate changes in demand for compute resources.

- **Application Load Balancer (ALB):** 
  - ALB distributes incoming requests across multiple EC2 instances to improve availability and traffic management.

- **Auto Scaling:** 
  - Automatically adjusts the number of EC2 instances in the backend API tier based on traffic ensuring that the system can handle spikes in demand and scale down during lower traffic periods.

- **Amazon RDS:** 
  - Manages the relational SQL database and automates tasks like backups, patching, and scaling.
  - Multi-AZ Deployment ensures high availability by replicating the database across multiple availability zones providing automatic failover if needed.

## 3. Ensuring Minimal Downtime

To keep downtime below two hours during migration, we will use the following approaches:

- **Database Migration:**
  - The SQL database will be transferred to Amazon RDS using the AWS Database Migration Service (DMS).
  - DMS supports continuous replication from the on-premises database to AWS ensuring data synchronization until the final cutover.

- **Blue-Green Deployment:**
  - We will set up the AWS environment in parallel with the on-premises infrastructure.
  - After testing and confirming that the AWS environment functions correctly, we will switch traffic from the on-prem system to AWS using Route 53, ensuring minimal downtime during this transition.

## 4. Data Consistency Strategy

To ensure data consistency throughout the migration process, the following steps will be taken:

- **Continuous Data Replication:**
  - AWS DMS will continuously replicate the SQL database, keeping the on-premises database synchronized with the new RDS instance during the migration.

- **Multi-AZ Deployment:**
  - Amazon RDS with Multi-AZ ensures automatic replication of data across different availability zones.
  - In case of an availability zone failure, the database will seamlessly fail over to the standby instance without data loss.

- **Final Synchronization:**
  - Before the final switch to AWS, a final synchronization will be performed to ensure no data loss and to maintain consistency across all users.

## 5. Step-by-Step Migration Process

1. **Preparation:**
   - Set up the AWS environment:
     - Create a VPC, subnets, and security groups.
     - Launch EC2 instances for both the frontend and backend.
     - Set up Amazon RDS with Multi-AZ enabled for the SQL database.

2. **Database Migration:**
   - Use AWS DMS to migrate the on-premises SQL database to Amazon RDS.
   - Enable continuous replication to minimize downtime.

3. **Application Migration:**
   - Deploy the frontend web application to EC2 instances.
   - Set up Auto Scaling and configure the ALB to manage incoming traffic.

4. **Testing:**
   - Thoroughly test the application and database in the AWS environment to ensure everything is functioning as expected.
   - Verify data consistency between the on-premises database and the new RDS instance.

5. **Final Sync and Cutover:**
   - Perform a final synchronization of the database using DMS.
   - Use Route 53 to switch traffic from the on-prem system to the AWS environment, ensuring a smooth transition with minimal downtime.

6. **Post-Migration:**
   - Monitor system performance and stability in the AWS environment.
   - Set up backup and disaster recovery protocols to safeguard the new infrastructure.


