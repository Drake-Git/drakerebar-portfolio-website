---
layout: page
title: "Azure Portfolio Deployment"
description: "Overcoming OIDC and CI/CD hurdles in Azure Static Web Apps."
---

# **This Website**


### **Overview**

This portfolio serves as a live demonstration of cloud infrastructure management and secure CI/CD practices. While the site itself is a lightweight implementation using **Jekyll** and the **Minima theme**, the underlying architecture is a purpose-built **Azure Static Web App (SWA)** integrated with **GitHub Actions**. The goal was to move beyond "one-click" deployments and build a repeatable, transparent pipeline.

### **Technical Challenges & Engineering Solutions**

The deployment process presented several critical hurdles that required deep-dive troubleshooting of the cloud handshake:

- **Authentication & Identity Handshake:** The native Azure setup defaults to an OIDC-based GitHub integration. However, due to configuration mismatches in the automated identity provider link, the deployment consistently failed during the "Event Info" validation. I diagnosed the failure by isolating the authentication function, eventually pivoting to a **Manual Deployment Token** method. This secured the link between GitHub and the Azure resource without relying on brittle automated wizards.
    
- **Pipeline Orchestration (Jekyll Integration):** The auto-generated GitHub Actions YAML lacked the necessary environment for a static site generator. I manually refactored the workflow to include **Ruby 3.4** initialization and **Jekyll build** steps.
    
- **Artifact Routing:** Following the build, the Azure engine failed to locate the `index.html` entry point. I resolved this by remapping the `app_location` and `output_location` paths within the YAML, ensuring the "delivery truck" was looking at the compiled `_site` folder rather than the raw source code.
    

### **Problems Overcome**

- **Credential/Handshake Mismatch:** Resolved by auditing SWA authorization policies and implementing direct API token authentication.
    
- **Workflow Schema Gaps:** Manually injected build dependencies (Ruby/Bundler) into the CI/CD pipeline.
    
- **Database Config Noise:** Eliminated "Data API" misconfiguration errors by explicitly defining null paths for non-existent backend resources.
    

### **The Path Forward**

- **Shift-Left Validation:** Transition from a "Push-to-Live" model to an **Azure DevOps** environment with a dedicated staging sandbox to validate builds before production deployment.
    
- **Infrastructure as Code (IaC):** Develop **Terraform** modules to automate the provisioning of the SWA, ensuring that infrastructure is version-controlled and reproducible.
    
- **Structured Troubleshooting:** Developing a repeatable "Cloud Triage Algorithm" to accelerate the identification of identity vs. connectivity issues in multi-cloud environments.

