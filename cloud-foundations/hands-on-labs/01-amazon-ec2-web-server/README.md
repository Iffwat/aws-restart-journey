# Lab 01 — Amazon EC2 Web Server

## Overview
This lab documents launching and managing an Amazon EC2 instance configured to host a basic web page.

> **Verification note:** Confirm every configuration value and step against your own training environment before treating it as a record of completed work. Training environments can differ.

## Objectives
- Launch and inspect an EC2 instance.
- Understand AMIs, instance types, storage, and networking.
- Configure inbound HTTP access with a security group.
- Use EC2 user data to automate basic web-server setup.
- Review instance health and monitoring.
- Understand instance resizing, EBS modification, and termination protection.

## Example configuration
Verify these values in your own lab before publishing:
| Setting | Example value |
|---|---|
| Instance name | Web Server |
| AMI | Amazon Linux 2023 |
| Instance type | t3.micro |
| vCPU / memory | 2 vCPU / 1 GiB |
| Key pair | No key pair (verify lab configuration) |
| VPC | Lab VPC |
| Security group | Web Server |
| Root EBS volume | 8 GiB |
| Termination protection | Enabled |

## 1. Launch the instance
1. Open the EC2 console in the assigned training environment.
2. Start the instance launch workflow.
3. Select the required AMI and instance type.
4. Configure the VPC, subnet, and security group as directed by the lab.
5. Review storage and advanced details.
6. Launch the instance and wait for it to reach the running state.

## 2. Configure Apache using user data
Example user-data script for Amazon Linux:

```bash
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```

User data can run commands during instance launch. Use the script specified or permitted by your actual lab.

## 3. Review health and monitoring
Inspect the instance state, system status checks, instance status checks, and available monitoring metrics in the EC2 console. Basic and detailed monitoring use different collection intervals; check the current AWS documentation and account settings.

## 4. Allow HTTP traffic
Example inbound rule:
| Type | Protocol | Port | Source |
|---|---|---:|---|
| HTTP | TCP | 80 | 0.0.0.0/0 (Anywhere-IPv4) |

Only use a public source range when required. In real deployments, restrict access to the smallest appropriate source range.

## 5. Test the web page
Once the instance and web-server service are ready:
1. Obtain the public IPv4 address or public DNS name if the lab provides one.
2. Open it in a browser using HTTP.
3. Confirm the expected page is displayed.

Expected example output:
```text
Hello From Your Web Server!
```

If it does not load, check instance health, security-group rules, routing, public addressing, and the web-server service.

## 6. Instance and EBS modification
The lab notes describe a resize exercise:
- Change the instance type from **t3.micro** to **t3.small**.
- Modify the root EBS volume from **8 GiB** to **10 GiB**.

Follow the lab's stop/start sequence and verify the final values. Changing an instance type generally requires the instance to be stopped. Increasing EBS capacity may also require expanding the partition and filesystem inside the operating system.

## 7. Termination protection
Termination protection helps prevent accidental termination through supported EC2 termination workflows. Test it only on the disposable training instance assigned to you. Disable it only when the lab instructs you to do so before cleanup.

## Key concepts
| Concept | Meaning |
|---|---|
| Amazon EC2 | AWS service for running virtual servers. |
| AMI | Image used as the basis for launching an instance. |
| Instance type | Defines compute resources such as CPU and memory. |
| Security group | Virtual firewall controlling allowed inbound and outbound traffic. |
| User data | Launch-time configuration commands or scripts. |
| Amazon EBS | Persistent block storage for EC2 instances. |
| Status checks | Checks that help identify instance or infrastructure issues. |
| Termination protection | Safeguard against accidental instance termination. |

## Evidence checklist
Add your own sanitized screenshots:
- [ ] `01-ec2-instance-running.png`
- [ ] `02-instance-configuration.png`
- [ ] `03-user-data.png`
- [ ] `04-ec2-status-checks.png`
- [ ] `05-cloudwatch-monitoring.png`
- [ ] `06-security-group-http.png`
- [ ] `07-web-server-output.png`
- [ ] `08-instance-resized.png`
- [ ] `09-ebs-volume-resized.png`
- [ ] `10-termination-protection.png`

Remove account IDs, credentials, session details, and other sensitive information before uploading.

## Further reading
- [Amazon EC2 User Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [EC2 user data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)
- [VPC security groups](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html)
- [EBS volume modifications](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-modify-volume.html)

## Reflection
After completing the lab, record what you configured, issues encountered, how you resolved them, and what you learned about EC2 networking, security, and storage.
