+++
comments = false 
date = "2015-06-22T00:00:00-00:00"
draft = false
share = false
slug = "resume"
title = "Resume"
+++

Email: [evandbrown@gmail.com](mailto:evandbrown@gmail.com)  
Website: [http://evanbrown.io](http://evanbrown.io)  
Phone: (206) 947-9338  
Address: 712 N 84th St, Seattle, WA 98103  
Twitter: [@evandbrown](https://twitter.com/evandbrown)  
GitHub: [evandbrown](https://github.com/evandbrown)  

---

## Summary

I&#x27;ve deployed software in rural Tanzania in search of a malaria vaccine, built APIs and infra in the cloud for an IoT startup before cloud and IoT were cool, and led developer advocacy programs for CloudFormation and Elastic Beanstalk at Amazon Web Services. I currently work at Google as a Senior Cloud Solutions Architect. In my free time I ride bikes, play with my daughter, and write tools in Go.

---

## Work

### Senior Cloud Solutions Architect, [Google](http://cloud.google.com)
##### September 2014 - present

I help customers run large-scale, reliable applications on Google Cloud Platform by working with engineers and architects to design, build, optimize, and operate infrastructure in the cloud. My specialties are systems automation, security, and migrating workloads to container-based deployments. In addition to helping customers build and deploy applications, I publish technical solutions and open source reference architectures to provide guidance and best-practices to a large audience.

For my 20% project I created (and currently maintain) the [`dm` tool](http://github.com/evandbrown/dm) for Google Cloud Platform's [Deployment Manager](https://cloud.google.com/deployment-manager/overview) service. Written in Go, `dm` is a tool with an opinion (not unlike `rake` or `make`) that makes managing large-scale cloud infrastructure not only super-efficient, but really fun.

### Senior Technical Program Manager, [Amazon Web Services](http://aws.amazon.com)
##### May 2011 - August 2014

I joined AWS as the company's first technical trainer. I developed the flagship [Architecting on AWS](http://aws.amazon.com/training/course-descriptions/architect/) course, trained over 1400 customer and partner engineers, and led internal train-the-trainer efforts to scale a global team of more than 20 trainers. I served as the principal trainer for AWS's key customers, inluding Intuit where I was the only technical trainer to receive a company-wide perfect evaluation.

In 2013 I moved internally to lead developer advocacy programs for CloudFormation and Elastic Beanstalk. I designed and built the first prototype of Docker support for Elastic Beanstalk, and helped drive it to [release](https://aws.amazon.com/blogs/aws/aws-elastic-beanstalk-for-docker/), marking the first official support for Docker at AWS. I was a regular conference speaker and held [weekly live Hangouts](https://plus.google.com/events/cbopt34eu8frvp5214u4l7c4sds) covering technical material and answering questions.

### Lead Software Engineer, Founding Team, [Enmetric Systems](http://www.enmetric.com)
##### February 2008 - April 2011

As the first software engineer on the founding team, I built the API for Enmetric's first product: a connected powerstrip that reports realtime energy usage metrics and can be controlled (plugs turned on and off) remotely. I was a strong advocate for cloud and automation from the first day. All production systems were deployed to EC2 and used S3 and Hadoop for data processing. New features were adopted as they were released by Amazon, including ELB and EBS.

I led the effort to embrace configuration management, choosing Chef as the tool to automate the build of all Amazon Machine Images used in the infrastructure. This allowed us to use Auto Scaling easily when it was released, and implement A/B tests long before they were en vogue.

### Bioinformatics Programmer, [Center for Infectious Disease Research](http://www.cidresearch.org/)
##### August 2005 - April 2011

Developed a proprietary laboratory management system (LMS) for the Center's Malaria Vaccine Initiative. The system used web services (Java and Spring) hosted in Seattle data centers and client software (Java Swing) deployed in Tanzania to record and track human tissue samples stored in the Tanzanian lab. Developed offline storage technology for client-side piece as power and network connectivity were spotty in remote labs. Guided FDA 21 CFR Part 11 audits to ensure compliance with good clinical practices.

Developed several internal business systems, including a .NET (C#) web application using MVC to calculate payroll distributions, as well as a system for managing billing for the Center's gene sequencing facility.

### Network Administrator, [The University of New Mexico Hospital](http://hsc.unm.edu/)
##### May 2001 - July 2005

Designed, developed and deployed intranet web applications (PHP) for ranking and evaluation of Medical Doctors in residency and fellowship programs. Administered Novell Network, Active Directory, and LDAP implementations for several clinical departments in the hospital. Manage DNS and marketing websites (including LAMP stacks) for several clinical departments in the hospital.

---

## Education

### University of New Mexico - B.S. in Biology and Chemistry
##### 2001 - 2004
GPA: 3.92

---

## Awards

#### Operational Excellence, Amazon Web Services
Received quarterly award (a fire extinguisher) by AWS SVP Andy Jassy for engineering operational excellence.

#### AWS Certified Solution Architect (Associate, 2013)

---

## Open Source Projects and Contributions

#### [dm](https://github.com/evandbrown/dm)
Golang. Author and maintainer. An opinionated tool for using the Deployment Manager service from Google Cloud Platform.

#### [Packer](https://github.com/mitchellh/packer/pull/1679)
Golang. Security contributions to GCE support in Packer.

#### [aMediaManager](https://github.com/awslabs/amediamanager)
Java/Spring. Primary author. Reference application for the [Develop, Deploy, and Manage Applications at Scale](http://www.amazon.com/Develop-Deploy-Elastic-Beanstalk-CloudFormation-ebook/dp/B00O96HVW6/ref=sr_1_1?ie=UTF8&qid=1436677346&sr=8-1&keywords=develop+deploy+and+manage) Kindle book, using CloudFormation, Elastic Beanstalk, S3, Elastic Transcoding Service, VPC, IAM, and other core AWS services.


---

## Publications and Blog Posts

#### [ Scalable and Resilient Web Applications on Google Cloud Platform](http://googlecloudplatform.blogspot.com/2015/03/introducing-the-Scalable-and-Resilient-Web-Apps-Solution.html)  
Primary author.

#### [Automated Compute Engine and Docker Image Builds with Jenkins, Packer, and Kubernetes](http://googlecloudplatform.blogspot.com/2015/05/Automated-Compute-Engine-and-Docker-Image-Builds-with-Jenkins-Packer-and-Kubernetes.html)
Primary author.

#### [Strong, Simple SSL for Kubernetes Services](http://blog.kubernetes.io/2015/07/strong-simple-ssl-for-kubernetes.html)
Primary author.

#### [Develop, Deploy, and Manage Applications at Scale](http://www.amazon.com/Develop-Deploy-Elastic-Beanstalk-CloudFormation-ebook/dp/B00O96HVW6/ref=sr_1_1?ie=UTF8&qid=1436677346&sr=8-1&keywords=develop+deploy+and+manage)

A Kindle book based on a comprehensive 5-part blog series covering best practices for automating complex infrastructure using CloudFormation and Elastic Beanstalk.

#### [Zero to Sixty: AWS Elastic Beanstalk](https://www.youtube.com/watch?v=Zb-lNr_TV2k) (re:Invent 2013)


#### [DockerCon 2014](https://www.youtube.com/watch?v=OzLXj2W2Rss)

High Fidelity, High Velocity Deployments in the Cloud

---

## Skills

* Advanced - Infrastructure Automation (AWS CloudFormation, Google Cloud Platform Deployment Manager, Jenkins)
* Advanced - Amazon Web Services (CloudFormation, VPC, IAM, EC2, S3, Elastic Beanstalk)
* Advanced - Google Cloud Platform (Compute Engine, Container Engine, Cloud Storage, EC2, S3, Elastic Beanstalk)
* Advanced - Go and Java
* Advanced - (except bisect) in Git
* Intermediate - Chef and Puppet
* Working Knowledge - Python, .Net, and Ruby
