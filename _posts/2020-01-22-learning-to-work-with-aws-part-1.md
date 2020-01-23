---
layout: post
title: Learning to work with AWS, Part 1
date: 2020-01-22 14:51 -0700
---

Nowadays, working knowledge of AWS or alternative cloud environment is a given for developers. Although AWS certifications are not required, bootcamp graduates who have relatively little industry experience should be equipped with the basic concepts and applications of cloud computing.

Today, I followed along this freecodecamp tutorial ([link](https://www.youtube.com/watch?v=3hLmDS179YE)) to set up a new AWS account (a great refresher course for those reconnecting with AWS). Initial setup included the following steps:

1. The Identity and Access Management (IAM): control access to AWS services and resources. Checkboxes included activating multi-factor authentication (MFA) on the root account, creating IAM users and assigning groups (such as admin) to them, and setting password policy.

2. Launch a new EC2 instance: select a free-tier-eligible option and get into it via the session manager instead of SSH (The session manager uses IAM for authentication and authorization, while SSH requires a key pair).

3. Set up budgets and alarms through CloudWatch.

4. Set up an application load balancer to evenly distribute traffic across multiple instances.


Topics on S3, CloudFront, Relational Database Service (RDS), and Lambda will be covered in the next post.


#### References
- A comprehensive article on AWS certifications by freecodecamp: https://www.freecodecamp.org/news/awscertified-challenge-free-path-aws-cloud-certifications/
- Intro to AWS by codeanalogies: https://dev.to/kbk0125/amazon-web-services-aws-explained-by-operating-abrewery-2j0
- Prepping for AWS Certified Cloud Practitioner exam: http://www.helenanderson.co.nz/aws-cloud-practitioner/
