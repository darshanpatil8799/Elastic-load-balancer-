<div align="center">

# 🚦 AWS EC2 + Elastic Load Balancer (ALB)

### Build a Highly Available Web Application with AWS

**Hands-on Project Documentation | By Darshan Patil**

![AWS](https://img.shields.io/badge/Cloud-AWS-orange?logo=amazonaws&logoColor=white)
![Amazon EC2](https://img.shields.io/badge/Compute-Amazon%20EC2-FF9900?logo=amazonec2&logoColor=white)
![Load Balancing](https://img.shields.io/badge/Networking-Elastic%20Load%20Balancing-232F3E?logo=amazonaws&logoColor=white)
![Status](https://img.shields.io/badge/Project-Completed-brightgreen)

</div>

---

## 📌 Project Overview

This project demonstrates how to deploy multiple Amazon EC2 instances and use an **Application Load Balancer (ALB)** to distribute incoming HTTP traffic between them.

The ALB provides a single DNS endpoint for users and forwards requests to registered targets in a target group. This setup helps demonstrate traffic distribution, target health monitoring, and a foundation for highly available web applications.

## 🎯 Objectives

- Launch multiple EC2 instances running Amazon Linux.
- Configure a security group for web access.
- Deploy a simple web page using EC2 user data.
- Create and register instances in a target group.
- Configure an Application Load Balancer and listener routing.
- Test the application through the load balancer's DNS name.

## 🧰 AWS Services Used

| Service | Purpose |
|---|---|
| **Amazon EC2** | Runs the web servers |
| **Application Load Balancer (ALB)** | Distributes incoming HTTP requests |
| **Target Group** | Registers EC2 targets and checks their health |
| **Security Groups** | Control inbound and outbound network traffic |
| **Amazon VPC** | Provides networking for the resources |
| **Availability Zones** | Allow resources to be placed across separate zones |

## 🏗️ Architecture

```text
                         🌐 Users / Browser
                                 |
                                 v
                    ┌────────────────────────┐
                    │ Application Load       │
                    │ Balancer (ALB)         │
                    └────────────────────────┘
                                 |
                         Listener: HTTP :80
                                 |
                                 v
                    ┌────────────────────────┐
                    │      Target Group      │
                    └────────────────────────┘
                         /       |       \
                        v        v        v
                   ┌────────┐ ┌────────┐ ┌────────┐
                   │ EC2-01 │ │ EC2-02 │ │ EC2-03 │
                   │ Web    │ │ Web    │ │ Web    │
                   │ Server │ │ Server │ │ Server │
                   └────────┘ └────────┘ └────────┘
```

## ⚙️ Implementation Steps

### 1. Configure a security group
- Open the **EC2 Dashboard → Security Groups**.
- Create a security group with a descriptive name.
- Configure only the inbound rules needed for your setup.

### 2. Launch EC2 instances
- Launch three Amazon Linux instances (the project guide uses `t2.micro` or `t3.micro`, subject to account and regional eligibility).
- Select the required VPC and subnet.
- Attach the appropriate security group.
- Add user data to install and start a web server and publish a simple test page.
- Wait until instance status checks pass.

### 3. Create a target group
- Open **EC2 → Target Groups** and choose **Create target group**.
- Select **Instances** as the target type.
- Configure the HTTP health check and port to match the web server.
- Register the EC2 instances and create the target group.
- Verify that the targets become healthy.

### 4. Create the Application Load Balancer
- Open **EC2 → Load Balancers → Create Load Balancer**.
- Select **Application Load Balancer**.
- Enter a name and choose the appropriate VPC and Availability Zones/subnets.
- Attach the ALB security group.
- Configure an HTTP listener on port `80` and forward requests to the target group.
- Create the load balancer and wait for its state to become **Active**.

### 5. Test traffic distribution
- Copy the ALB DNS name from the AWS console.
- Open it in a browser using `http://<your-load-balancer-dns>`.
- Refresh the page several times. If each target serves a distinguishable response, you can observe requests being handled by different instances.
- Check target health in the target group.

## 🔐 Security Notes

For a safer configuration:

- Allow inbound **HTTP (port 80)** to the ALB security group when serving a public HTTP test page.
- Allow inbound **web-server traffic from the ALB security group only** to the EC2 instance security group.
- Restrict **SSH (port 22)** to your trusted IP address; do not expose it to everyone.
- Use HTTPS with a suitable certificate for production traffic.
- Do not use public access rules more broadly than the project requires.

> **Important:** The project guide mentions SSH, HTTP, and HTTPS inbound rules. For a typical ALB design, users access the ALB, and the EC2 instances accept application traffic from the ALB security group. Open HTTPS (443) on the ALB only when HTTPS is configured.

## 🧪 Validation Checklist

- [ ] All EC2 instances are running and pass status checks.
- [ ] The target group contains the intended instances.
- [ ] Target health checks report healthy targets.
- [ ] The ALB state is **Active**.
- [ ] The ALB DNS name loads the test web page.
- [ ] Different instance responses can be identified, if configured.

## 💡 Key Learnings

- Understanding the role of a load balancer in a cloud architecture.
- Launching and configuring EC2 web servers.
- Working with target groups, listeners, and health checks.
- Understanding how ALB DNS routes traffic to registered targets.
- Practicing foundational availability, scalability, and security concepts.

```
.
├── README.md
└── screenshots/
    ├── ec2-instances.png
    ├── target-group-health.png
    ├── alb-configuration.png
    └── website-test.png
```

## 💰 Cost Awareness

AWS resources may incur charges, including EC2 instances, load balancers, and data transfer. Charges and Free Tier eligibility depend on your account, region, resource type, and current AWS terms. Review pricing before deployment and delete resources when you have finished testing.

## 🔭 Future Enhancements

- Configure HTTPS using AWS Certificate Manager.
- Add an Auto Scaling Group to manage EC2 capacity.
- Add CloudWatch metrics and alarms.
- Deploy a sample application with health-check endpoints.
- Explore multi-AZ design and failure testing.

## 👨‍💻 Author

**Darshan Patil**  
Cloud & DevOps Learner

- GitHub: [Darshan Patil](https://github.com/darshanpatil8799/darshanpatil8799)
- LinkedIn: [Darshan Patil](www.linkedin.com/in/darshan-devops)

---

<div align="center">

### 🌟 Learn. Build. Test. Improve.

**Building practical AWS skills, one project at a time.**

</div>
