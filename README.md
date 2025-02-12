# Final Project Overview

Welcome to the Final Project! This capstone assignment is your opportunity to showcase the skills you've developed over the course of this class. You'll deploy, configure, and manage a real-world application using Docker and CI/CD pipelines. This project emphasizes containerization, automation, and best practices in modern software development.

---

## Project Options

For your final project, you can choose one of the following options:

### 1. **Deploy a Saleor Dashboard**

Containerize and deploy the [Saleor Dashboard](https://github.com/cypher4859/codeyou-devops-with-aws-final-project-saleor-full), a powerful headless e-commerce platform. Additional challenges:

- **Bonus 1**: Deploy the [Saleor Storefront](https://github.com/saleor/storefront) alongside the dashboard.
- **Bonus 2**: Integrate Jaeger for distributed tracing (accessible on port 16686).
- **Bonus 3**: Integrate Mailpit for testing email functionality (accessible on port 8025).

[**Learn More**](https://github.com/cypher4859/codeyou-devops-with-aws-final-project-saleor-full)\
*Link to detailed Saleor documentation.*

### 2. **Bring Your Own App (BYOA)**

Develop and deploy your own application as part of your capstone project. This option is flexible and suitable for:

- Software development students building custom applications.
- Graduated students revisiting their capstone projects for real-world deployment experience.

---

## Deliverables

Each final project must include the following deliverables:

### 1. **Docker Compose Configuration**

- Provide a `docker-compose.yml` file that enables local deployment of your project.

### 2. **Dockerfile**

- Include a `Dockerfile` for each custom image required for your stack.

### 3. **Repository Structure**

- Maintain the following branches:

#### `develop`

- **Purpose**: Active development environment.
- **Pipeline Requirements**:
  - Linting and static code analysis.
  - Security and dependency checks.
  - Deploy an image tagged as `<your-app-name>:develop`.

#### `staging`

- **Purpose**: Integration and testing environment.
- **Pipeline Requirements**:
  - Execute application tests.
  - Validate service startup using `docker-compose up` or health checks.
  - Deploy an image tagged as `<your-app-name>:staging`.

#### `production`

- **Purpose**: Production-ready environment.
- **Pipeline Requirements**:
  - Deploy an image tagged as `<your-app-name>:production`.
  - Maintain a `latest` tag reflecting the production environment.
  - Ensure this branch is used for deployment to AWS.

### 4. AWS Deployment

- Your project must be deployed to Amazon ECS (Elastic Container Service).

- Provide the necessary configurations for ECS deployment, including:
    - ECS Cluster using either Fargate (recommended) or EC2 Container Instances.
    - ECS Task Definition(s). One Task Definition is recommended that handles all of your containers but it's up to you.
    - ECS Service configuration that uses either EC2 or Fargate (recommended)
    - Networking settings (VPC, subnets, and security groups). It's recommended though not required to use the following:
      - Default `-` VPC
      - Subnets within the default VPC:
        - `subnet-0243668670d02534c`
        - `subnet-021d0e5aee26923da`
        - `subnet-03224a2574b748db6`
      - Load Balancer of `Default-App-Load-Balancer`

**OPTIONAL**: Deploy with EC2 Container Instances  
Should you be taking this route then you will probably need to use the following:
   - Networking settings (VPC, subnets, and security groups). It's recommended though not required to use the following:
      - Default `-` VPC
      - Subnets within the default VPC:
        - `subnet-0243668670d02534c`
        - `subnet-021d0e5aee26923da`
        - `subnet-03224a2574b748db6`
      - Load Balancer of `Default-App-Load-Balancer`
  - You'll need to create a Launch Template for the specs of the machine that your ECS Task will be placed on.
  - You'll need to create an Autoscaling Group that uses the Launch Template
  - You'll need to add a Capacity Provider to your ECS Cluster and specify the Autoscaling Group
  - Then you'll proceed with creating the ECS Service and so forth. Once you specify that the Service should have +1 Tasks then the Service should automatically create the EC2 machine and place the Task.
  
**ALTERNATE: ECS via EC2 Container Instances Deployment**  
You could avoid needing a launch template and autoscaling group if you manually create an EC2 machine and register it with your ECS Cluster. Bear in mind that this could be more difficult than the original Fargate option.

Ensure the deployed application is accessible and functional in the AWS environment.

**NOTE: The grade depends on the deployment working, not the Application code so if the app doesn't totally work but the deployment succeeds and the containers are running then that's all you need to focus on.**

---

## CI/CD Requirements

- A successful CI/CD pipeline must exist for each branch (`develop`, `staging`, `production`):
  - **Linting and Static Code Analysis**: Use tools like Ruff or Flake8.
  - **Security and Dependency Analysis**: Use tools like `pip-audit`.
  - **Vulnerability Scanning**: Use Trivy to scan Docker images.
  - **Build and Test Docker Images**: Verify that the application image is functional.
  - **Push to DockerHub**: Automate image deployment to DockerHub with appropriate tags.

---

## Notes and Additional Challenges

### All Projects

- Your project deployed must operate within a 1.5GB memory limit. If you're concerned then we can talk about it but I don't think this will impact anyone
- Ways to test this: Bring up your docker-compose stack, make sure everything is working, and run `docker stats` to evaluate how much memory your stack is running.

### Saleor Dashboard

- **Bonus Challenges**:
  - Deploy the Saleor Storefront alongside the dashboard.
  - Integrate Jaeger and confirm it is accessible on port 16686.
  - Integrate Mailpit and confirm it is accessible on port 8025.

### BYOA

- Use this option to align the project with your capstone goals.

---

Best of luck with your final project! Remember to follow best practices and have fun learning!

