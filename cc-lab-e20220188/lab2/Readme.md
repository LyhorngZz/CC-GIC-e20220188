# Cloud Lab 2 Submission — Load Balancer and Auto Scaling

- **Student name:** Hun Lyhorng
- **Student ID:** e20220188
- **Learner Lab user name:** HUN_LYHORNG
- **Date completed:** 05/11/2026

---

## Security groups

![LoadBalancerSecurityGroup](images/01-sg-load-balancer.png)

![LaunchTemplateSecurityGroup](images/02-sg-launch-template.png)

## Target group

![LoadBalancerTargetGroup](images/03-target-group.png)

![Health checks](images/04-health-checks.png)

## Application Load Balancer

![Load balancer list](images/05-load-balancer-list.png)

![Load balancer details](images/06-load-balancer-details.png)

## Launch template

![AutoScalingLaunchTemplate](images/07-launch-template.png)

## Auto Scaling group

![Auto Scaling groups](images/08-asg-list.png)

![Auto Scaling group details](images/09-asg-details.png)

## Load balancing test

![First request](images/10-browser-1.png)

![Second request, different host](images/11-browser-2.png)

## Simulated application failure

![Stopping httpd](images/12-stop-httpd.png)

![Target unhealthy or draining](images/13-target-unhealthy.png)

![New target healthy](images/14-target-replaced.png)

---

## Questions and Answers

1. Why does the page show a different host name when you refresh it?

    Because the load balancer distributes requests across different healthy EC2 instances, each with its own host name.

1. Why was the instance marked unhealthy after stopping httpd?

    The health check tests whether the web server responds to HTTP requests on port 80. After stopping httpd, the server could no longer respond, so the target became unhealthy.

2. Who replaced the failed instance?

    The **Auto Scaling** group replaced it.
    - Load Balancer: Distributes incoming traffic.
    - Target Group: Checks instance health.
    - Auto Scaling Group: Replaces unhealthy instances.

3. How many instances normally run? When could there be 3?

    Normally, 2 instances run because the desired capacity is 2. There could temporarily be 3 during instance replacement or when scaling out, without exceeding the maximum capacity.

4. How can instances accept HTTP only from the load balancer?

    Change the HTTP inbound rule in LaunchTemplateSecurityGroup from Anywhere-IPv4 to the security group ID of LoadBalancerSecurityGroup. This allows HTTP traffic only from the load balancer.