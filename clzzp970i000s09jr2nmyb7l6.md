---
title: "FOXHOUND-DevLog: 001"
seoTitle: "FOXHOUND DevLog 001"
seoDescription: "Explore cloud projects with FOXHOUND-DevLog: automated infrastructure, AWS Cognito, API Gateway, budget management. Subscribe for updates"
datePublished: Sun Aug 18 2024 15:06:03 GMT+0000 (Coordinated Universal Time)
cuid: clzzp970i000s09jr2nmyb7l6
slug: foxhound-devlog-001
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/_iNpDEGu_UE/upload/7dc226704465adbf131fef71adfece81.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1723993521133/3e829c89-a6c0-49bc-8057-8c1395691223.png
tags: aws, architecture, automation, infrastructure, infrastructure-as-code, pulumi

---

## TLDR

Welcome to "FOXHOUND-DevLog," a tech series exploring cloud projects using automated mechanisms. We'll cover infrastructure as code, new technologies, and efficient workflows. Our initial design uses AWS, GitHub Actions, Pulumi, and Doppler for secrets management. We have two flows: Infra-Dev for deploying AWS infrastructure and Client for using it via a CLI app. AWS Cognito handles authentication, and API Gateway with Lambda functions backed by S3 serves as our makeshift database. Budget alarms will help manage costs. Future entries will cover infrastructure code, Swagger docs, SAST in CICD, and WAF rules. Subscribe for updates.

## **Welcome to FOXHOUND-DevLog**

Watch me create this design on my YouTube channel. Make sure to subscribe as these blogs will go along with a corresponding video [here](https://youtu.be/ZgvX0a1Pqe8)

%[https://youtu.be/ZgvX0a1Pqe8] 

Hey everyone, welcome to the newly refreshed tech series "FOXHOUND-DevLog," where we will explore creating cloud projects using fully automated turnkey mechanisms. These articles follow a series of YouTube videos available on my channel [You Suck At Cloud](https://www.youtube.com/@F%C3%98XH%C3%98UND79-79). The goal is to provide a series of blogs and videos demonstrating the power of infrastructure as code, new technologies I experiment with, and discoveries on how to work more efficiently. We will cover topics like cloud, programming, useful tips, and new tech. Think of this as "If you don't like watching videos, you can just read it here." Make sure you subscribe to stay updated whenever a new post is created.

## **Initial Design Blueprint**

%[https://snappify.com/view/942a91a6-1c0d-4560-8de3-ead5cd01a08a] 

In our initial design, we are working within a single AWS account that authenticates to perform infrastructure maintenance via a GitHub Actions runner using Pulumi (Go) as our infrastructure as code tool. In later videos, we will integrate the Pulumi flow to retrieve AWS credentials for `role assumptions` with a custom `IAM Policy` using my favorite secrets management platform, `Doppler`. However, this will be covered in another entry in this series.

#### **Infrastructure Deployment and Client Interaction**

Beyond the provisioning flow, we are building two flows here: a `Client` flow and an `Infra-Dev` flow. The Infra-Dev flow deploys the AWS infrastructure, and the Client flow uses that infrastructure. The `Client` will use a CLI-based application that we will write using Go and `Cobra` to interface with our CLI. The CLI will have API endpoints for logging into AWS Cognito to perform Proof Key for Code Exchange (PKCE), and then make authenticated calls to the API Gateway.

#### **Secure Authentication with AWS Cognito**

AWS Cognito will have a domain backed by `ACM` (Amazon Certificate Manager), which interfaces with our primary DNS zone hosted on Cloudflare. The cool part is that we can create the CNAMEs on the fly with our Pulumi deployment, tying these services together.

Inside of AWS Cognito we are going to create a `user-pool` and a client. This will allow us to onboard a mock user in order to perform the PKCE(Proof Key for Code Exchange) to generate the token on our local machine and store that token inside of our (my) OSX Keychain for safe keeping. Don't worry, I will walk you through the code that does the storing and retrieval of this key.

#### **Simplified Data Management with S3 and Lambda**

Next, the API Gateway will be backed by a series of Lambda functions. These functions will interact with AWS S3, which we will use as a makeshift database. The reason for choosing S3 over DynamoDB is its convenience and ease of use at this stage of development. Each Lambda function will handle specific tasks such as data retrieval, storage, and processing. By using S3, we can store data in a flexible and scalable way without the need to set up and manage a more complex database system. This setup allows us to quickly prototype and iterate on our application while keeping the infrastructure simple and manageable.

#### **Keeping Costs in Check with Budget Alarms**

Being budget-conscious is crucial, as it is one of the pillars of the AWS Well-Architected Framework. I need to create budget alarms to alert us when spending approaches predefined limits, helping us shut down infrastructure to avoid unnecessary costs during inactivity. These alarms allow real-time spending monitoring and proactive cost management. Notifications via email or SMS enable quick responses and informed decisions about scaling down resources or optimizing usage. Plus, I am *not* made of money, and I guess neither are you. *laughs and cries that I am not Jeff Bezos*

In the next entry, we will cover how to create AWS budget alarms using Pulumi. This will enable you to codify these budgets as part of your entire deployment stack, ensuring that cost management is integrated into your infrastructure from the start. I will walk through the steps to define budget thresholds, set up notifications, and automate the process of shutting down resources when necessary. This approach will help you maintain control over your expenses and adhere to best practices for cost management in the cloud.

#### **Multi-Channel Budget Alerts**

Now, when setting up alarms for the budgets themselves, we need to ensure they are sent to multiple destinations to maximize our chances of noticing them promptly. The first destination is email, which is a standard and reliable method for receiving alerts. The second destination is directly to our phones via SMS, ensuring that we get immediate notifications even when we are away from our computers. The last destination is a Slack workspace, which is particularly useful for teams that use Slack for daily communication. By receiving alerts in Slack, Let's be honest, the more places I see an alert, the more likely I am actually going to do something about it. This multi-channel approach ensures that budget alarms are hard to miss, helping us stay on top of our spending and avoid unexpected costs.

#### **Experimentation and Learning**

It's important to understand that these are `personal` projects that are meant to just expand our skills and perform experimentation. They are not production level systems that will be handling hundreds of thousands of requests, they are literally only going to be handling a single user. So with that in mind, we are not focused on things like Caching, Rate Limiting, or DR/HA at this time. We might in future entries into the DevLog consider looking at those things for a fun experiment, but that the moment, let's just get a working model deploy mmkay? Coooool.

#### **What's Next: Upcoming Topics and Code**

Cool, next you are asking “This is cool, but where is code? How can I try this?!?!?” Well slow your roll, speed racer. In the next few entries we will be covering the following, then we will go from there. So if this has caught your interest, make sure that you subscribe to the newsletter.

* The Infrastructure Code
    
* Creating A Swagger Doc
    
* Implementing SAST in the CICD
    
* Creating WAF Rules