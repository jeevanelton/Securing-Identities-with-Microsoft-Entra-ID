Microsoft Azure Basics: Securing Identities with Microsoft Entra ID

Scenario

I have just joined Contoso Ltd. as a junior Cloud Security Engineer. The company is moving its workforce to the cloud and uses Microsoft Entra ID (formerly Azure Active Directory) as its identity provider.

my manager hands me a task:


"We are onboarding a new finance team. I need to create their accounts, organize them into a group, give them only the access they need (least privilege), force them to use Multi-Factor Authentication (MFA), and block any risky sign-ins from outside our country. Finally, show me I can review the sign-in activity to confirm everything is working."



In this project, I will play the role of that engineer and secure the identities of the new finance team step by step.

Introduction

In this project, I'll learn how to secure identities using Microsoft Entra ID on Microsoft Azure. Identity is the new security perimeter in the cloud, if an attacker steals a valid identity, network firewalls won't stop them. We'll cover creating users and groups, assigning roles using Role-Based Access Control (RBAC), enforcing Multi-Factor Authentication, building a Conditional Access policy, and reviewing sign-in logs for monitoring.

Pre-requisites


Basic understanding of cloud computing and identity concepts
A Microsoft Azure account (free tier / free trial available)
An Entra ID tenant with Global Administrator or Security Administrator rights (my free tenant gives this by default)
A Microsoft Entra ID P1 or P2 license to use Conditional Access (a free P2 trial is available; otherwise I can apply Security Defaults as the fallback — noted in Exercise 4)


Lab Set-up and Tools


Azure Account: Sign up for a free Azure account if I don't have one.
Azure Portal: Access to the Azure Portal.
Microsoft Entra admin center: Access to the Entra admin center.
Azure CLI (optional): Install the Azure CLI on my local machine for the command-line exercise.
