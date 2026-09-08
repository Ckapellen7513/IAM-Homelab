# IAM-Homelab
Hybrid Enterprise IAM Lab: Azure AD DS to Okta Identity Cloud Integration
# Hybrid Enterprise IAM Lab: Azure AD DS to Okta Identity Cloud Integration

![Architecture Diagram](./diagrams/hybrid-iam-architecture.png)

## Overview
This project demonstrates the design, deployment, and configuration of an enterprise-grade hybrid identity architecture. An Active Directory Domain Services (AD DS) environment hosted on an Azure Virtual Machine serves as the primary Directory Source of Truth, integrated seamlessly with an Okta Identity Cloud tenant using the Okta AD Agent. 

The lab simulates real-world enterprise Identity and Access Management (IAM) workflows, including directory synchronization, schema mapping, delegated authentication, and automated lifecycle management.

---

## Technical Specifications & Stack
* **Directory Source of Truth:** Active Directory DS (`iam-homelab.local`)
* **Cloud Infrastructure:** Azure Virtual Machine (`IAM-Homelab`, Windows Server 2022)
* **Identity Provider (IdP):** Okta Universal Directory (Developer Edition)
* **Integration Component:** Okta Active Directory Agent (v3.23.0)
* **Protocol Support:** LDAP, Kerberos/NTLM (Delegated Auth), HTTPS (TLS 1.2/1.3 Outbound)

---

## Architecture & Data Flow

```mermaid
graph TD
    subgraph Azure Cloud Environment
        VM[IAM-Homelab VM<br/>Domain Controller]
        ADDS[(Active Directory DS<br/>iam-homelab.local)]
        Agent[Okta AD Agent<br/>v3.23.0]
        
        VM --- ADDS
        ADDS <-->|LDAP / Kerberos| Agent
    end

    subgraph Okta Identity Cloud
        UD[(Okta Universal Directory)]
        Apps[Enterprise SaaS Apps<br/>SAML / OIDC]
        
        UD <--> Apps
    end

    Agent -->|Outbound HTTPS / Port 443| UD


