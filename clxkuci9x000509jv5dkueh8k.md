---
title: "Azure Resource Groups: A Beginner's Journey"
seoTitle: "Azure Resource Groups Guide for Beginners"
seoDescription: "Beginner's guide to Azure Resource Groups: logical containers, resource providers, and Azure Resource Manager explained. Watch the0x explain on youtube"
datePublished: Tue Jun 18 2024 20:12:38 GMT+0000 (Coordinated Universal Time)
cuid: clxkuci9x000509jv5dkueh8k
slug: azure-resource-groups-a-beginners-journey
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ttj0x50eFEs/upload/84e063f496b7fa0c311f2fb5fdaea01f.jpeg
tags: azure, pulumi

---

%[https://youtu.be/g0Ke-dcEj_Q] 

Ah, the start of something new. Isn't it great? What are we learning about you might ask? Well.... Ya boy has not touched Azure in about 3 years, and I just so happen to have a itch to get up-skilled in something that I don't really touch in my day to day. So why not create a blog series about topics as I learn about them? I can provide some code snippets and some diagrams. I am also create 5-10 minute youtube videos to help those who rather watch my pretty face explain these topics as I learn about them. You can find that on the [You Suck At Cloud Youtube Channel](https://www.youtube.com/channel/UCB0Yt1I6UQGHw9CMniq_8Wg) or follow my voice on [Spotify](https://open.spotify.com/show/7gieKpIDrp1qUI0zR9fDE6?si=e665b06361414084)

### The Goods

%[https://snappify.com/view/5ab3a2dc-4b94-4f8a-90b7-4da2f9a49c8b] 

#### What Are Resource Groups

Alright, today we are discussing **Azure Resource Groups.** Resource Groups are logical containers which allow azure administrators to work with sets of *resources* (infrastructure objects) in your architecture as a single maintained solution. Resource groups are defined within Azure Subscriptions to act as a single contained billing unit.

#### What is a Resource?

A resource is a single infrastructure object. This can be a virtual machine, a storage account, a network component. These objects can be grouped together by a variety of logical reasons to come to what is called a resource group.

#### What Are Azure Resource Providers

Azure resource providers are a service that offer capabilities to manage and interact with the various type of azure *resources* such as virtual machines, storage accounts, networking components and so forth. Each provider is responsible for the creation, updating, and deletion actions performed on the targeted resources. For example, the *Microsoft.Compute* provider is responsible for all virtual machines. The provider works very closely alongside the ARM.

#### Azure Resource Manager (ARM)

The Azure Resource Manager acts as a orchestration mechanism for deployment and management of the targeted/deployed objects (resources) in the azure environment. ARM acts as a coordination point allowing for handling of all API requests, and routing them to the appropriate resource provider.

#### Laymans Terms

When we write pulumi or terraform code in our cloud lab we execute that code and the code is converted to a series of API calls to the ARM. The ARM then takes those calls and dishes them out to the resource provider, who will then perform the necessary actions against the targeted resources. Either making a new resource, updating an existing one or deleting a resource all together.

#### Conclusion.

Alright, hope that was straight forward enough, see ya in the next entry of the series Where we will discuss a method of deployment called "Resource Templates"