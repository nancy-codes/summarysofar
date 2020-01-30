---
layout: post
title: VPC in the Cloud, Part 3
date: 2020-01-29 21:24 -0700
---
In the AWS cloud, you can set up a software-defined network called virtual private cloud (VPC). Similar to a physical network, each VPC has its own IP addresses, subnets, route tables, and firewalls. You can organize your multiple instances by locking them in a VPC and set up a different network configuration for each cluster of instances, like so:

<img src="https://user-images.githubusercontent.com/24424825/73419844-db240d00-42dd-11ea-8a18-8e21d3721130.png" width="60%" style="display:block; margin-left:auto; margin-right:auto;">

<br>
VPC is there to protect your resources. Without such system in place, all of your resources in your AWS account are exposed to the public Internet unguarded. Apparently, AWS used to be lacking this security feature until it enforced a VPC by default for every new instance in 2009. With VPC, you can have control over what traffic you want to allow or deny to reach your resources.

This also means that you would need to configure some stuff. Specifically, you will be prompted to select the IP address range, create subnets, configure route table, set up network gateways, define security setting using security groups and network access control lists (ACLs). Lots of AWS lingos and design concerns here. These concepts will make a lot more sense when you actually apply to your application. So now it is your turn to [sign into your console](https://aws.amazon.com/) and create your own custom VPC.


**References**
- [AWS Tutorial for beginners](https://www.youtube.com/watch?v=fpxDGU2KdkA)
- [Core concepts in VPC](https://gruntwork.io/guides/networking/how-to-deploy-production-grade-vpc-aws/#what-is-a-vpc)
- [Practical VPC Design](https://medium.com/aws-activate-startup-blog/practical-vpc-design-8412e1a18dcc)
