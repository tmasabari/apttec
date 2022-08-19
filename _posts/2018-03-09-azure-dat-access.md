---
layout: post
title: Azure data access
date: 2018-03-09 16:39
author: tmasabari
comments: true
categories: [Uncategorized]
---
<strong>What is the difference between SQL Server on Azure VM and Azure SQL Database?</strong>

[table id=5 /]

<strong>An application front end is hosted on Azure but due to security reasons customer want database to be hosted on-premises within his office building. </strong><strong>What are the different ways to handle this connectivity scenario in Azure?</strong>

Looking at the requirement of connecting single on premises DB machine to Azure hosted application, Azure VNET based “Point to Site” can be considered as correct choice in this scenario for Azure to on premises connectivity. Point to Site is ideal choice for establishing VPN connectivity between on premises resources and Azure resources where number of resources to be connected is limited.

<strong>What are the other VNET options for achieving connectivity with on premise and azure resources?</strong>

Site to Site and express route are other options for achieving cross premises connectivity. Site to site to specifically use when you have large number of resources to be connected.

In some cases, Site to Site or Point to Site connectivity may introduce network latency as VPN created by these features work on public infrastructure (Internet) only. To overcome on this situation “Express Route” option can be taken which offers dedicated Leased Line based offering to overcome on latency issue.

<strong>What is the option to connect on premises Database in case user is not willing to open up VNET based connectivity?</strong>

In such case, a WCF service can be developed and hosted on premises. This WCF service will have CRUD operations specifically against the on premises database. Then Service bus relay option can be used for invoking on premises WCF service from Azure hosted web application to access the database. Use of WCF and service bus relay will avoid the option of VPN connectivity using Azure VNETs offerings.

&nbsp;

&nbsp;
