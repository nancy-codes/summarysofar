---
layout: post
title: Amazon S3, Part 2
date: 2020-01-25 11:56 -0700
---

#### Overview
S3 stands for Simple Storage Service.

Amazon S3 is a cloud storage service known for its super durability and industry-leading scalability. Several use cases include hosting static resources of your web applications such as media files (i.e., .txt, .png, .mp4, .mp3, .zip, etc), online backup and restore, archive, and big data analytics, just to name a few. To get a feel for how Amazon S3 buckets work, follow this tutorial [link](https://www.qwiklabs.com/focuses/8582?catalog_rank=%7B%22rank%22%3A3%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=4411966) that covers the following topics:

- Create a bucket in Amazon S3
- Add an object to your bucket
- Manage access permissions on an object
- Create a bucket policy using the Policy generator
- Use bucket versioning



#### Some facts about Amazon S3 buckets

- Once you sign up on AWS, you get a year of free usage. That means that you get 5GB of S3 storage, 20000 GET requests, 2000 PUT, COPY, POST, LIST requests, and 5 GB data transfer in and out every month.
- You can create up to 100 buckets in each of your AWS accounts.
- Each bucket is region-specific. By default, it will be in your current location of your AWS, as uploading a file to the closest data center will optimize latency, minimize costs, or address regulatory requirements.
- Each bucket name must be unique, as it makes up part of your S3 url (aka, `https://s3-<region>.amazonaws.com/yourbucketname`).

There are a couple of S3 client tools (FTP clients that allow you to connect to Amazon S3 for our purposes). Options include CrosssFTP Pro, FileZilla Pro, Cyberduck, S3 Browser, Cloudberry, etc. Most of them are paid services, but if you are looking for free options, try either S3 Browser or Cyberduck.



#### References
- https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingBucket.html
- https://medium.com/@lewisdgavin/aws-s3-overview-6fe9ca2a1e0a
