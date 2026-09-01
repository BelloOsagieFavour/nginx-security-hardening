# NGINX Security Hardening & Patching

## Project Overview

This project documents an internal security assessment of an outdated NGINX web server running NGINX v1.15.5. The assessment examined the security risks associated with an outdated installation, insecure package retrieval, manual compilation, SSH exposure, missing integrity verification, and weak TLS defaults.

The project also documents using Ansible to automate NGINX updates and verify the resulting installation.

## Assessment Type

**Internal Security Assessment**

**Target:** NGINX Server (v1.15.5)

**Risk Level:** Critical

## Objectives

- Assess the security risks of an outdated NGINX installation.
- Identify vulnerabilities and insecure deployment practices.
- Document NGINX installation and configuration validation.
- Apply remediation recommendations.
- Use Ansible to automate NGINX patching and verification.

## Environment Preparation

The assessment included preparation of the environment and SSH configuration. The report documents installation and startup of OpenSSH Server and the use of the Kali archive keyring for trusted package installation.

## NGINX Deployment

The assessment documented downloading NGINX 1.15.5, installing build dependencies, extracting the source code, compiling and installing NGINX, starting the service, and validating the configuration.

Key commands documented in the report include:

```bash
wget http://nginx.org/download/nginx-1.15.5.tar.gz
apt install build-essential libpcre3 libssl-dev
tar -zxvf nginx-1.15.5.tar.gz
./configure
make
make install
/usr/local/nginx/sbin/nginx
sudo /usr/local/nginx/sbin/nginx -t
```

## Vulnerability Assessment

The report identified the following security issues:

| Finding | Risk | Recommended Remediation |
|---|---|---|
| Outdated NGINX version | Critical | Upgrade to the latest stable NGINX release |
| Multiple NGINX vulnerabilities | High | Upgrade to the latest stable NGINX release |
| HTTP download | High | Use HTTPS for package downloads |
| Missing integrity verification | High | Verify GPG signatures before installation |
| SSH exposure | Medium | Restrict SSH access using firewall rules |
| Manual compilation | Medium | Use package manager installations for updates |
| Weak TLS defaults | Medium | Use strong cipher suites and disable weak ones |

## Ansible Patching

The project documents installing Ansible, verifying the installation, creating an `update_nginx.yml` playbook, executing it with elevated privileges, and verifying the NGINX version afterward.

Example commands:

```bash
sudo apt install ansible -y
ansible --version
nano update_nginx.yml
ansible-playbook update_nginx.yml --ask-become-pass
nginx -version
```

## Evidence 
## Evidence

The following evidence documents the deployment, assessment, and automated patching of the NGINX server.

### 1. Kali Linux Environment Preparation

![Kali Linux Environment Preparation](screenshots/nginx-report-image-1.png)

Initial environment preparation and trusted Kali package key configuration.

### 2. SSH Service Installation and Verification

![SSH Service Installation and Verification](screenshots/nginx-report-image-2.png)

SSH was configured and verified as an active service.

### 3. Downloading the Outdated NGINX Version

![Downloading NGINX 1.15.5](screenshots/nginx-report-image-3.png)

The assessment downloaded the outdated NGINX 1.15.5 source package for security evaluation.

### 4. Installing NGINX Build Dependencies

![NGINX Build Dependencies](screenshots/nginx-report-image-4.png)

Required compilation and development dependencies were installed.

### 5. Extracting the NGINX Source Code

![Extracting NGINX Source Code](screenshots/nginx-report-image-5.png)

The NGINX 1.15.5 source archive was extracted for compilation.

### 6. Compiling and Installing NGINX

![Compiling and Installing NGINX](screenshots/nginx-report-image-6.png)

NGINX was configured, compiled, and installed from source.

### 7. Starting the NGINX Server

![Starting NGINX Server](screenshots/nginx-report-image-7.png)

The manually installed NGINX server was started successfully.

### 8. NGINX Configuration Validation

![NGINX Configuration Validation](screenshots/nginx-report-image-8.png)

The NGINX configuration was tested and confirmed to have valid syntax.

### 9. Initial NGINX Version Verification

![Initial NGINX Version](screenshots/nginx-report-image-9.png)

The installed server was verified as NGINX 1.15.5, confirming the outdated version.

### 10. Nessus Vulnerability Assessment – NGINX

![Nessus NGINX Vulnerability Assessment](screenshots/nginx-report-image-10.png)

Nessus identified multiple vulnerabilities associated with the outdated NGINX installation.

### 11. Nessus Vulnerability Assessment – ImageMagick

![Nessus ImageMagick Vulnerability Assessment](screenshots/nginx-report-image-11.png)

Additional vulnerabilities identified during the Nessus security assessment.

### 12. Nessus Vulnerability Assessment – SSL

![Nessus SSL Vulnerability Assessment](screenshots/nginx-report-image-12.png)

SSL-related vulnerabilities identified during the vulnerability assessment.

### 13. Installing Ansible

![Installing Ansible](screenshots/nginx-report-image-13.png)

Ansible was installed to automate the NGINX patching process.

### 14. Verifying Ansible Installation

![Ansible Version Verification](screenshots/nginx-report-image-14.png)

The installed Ansible version was verified successfully.

### 15. Creating the NGINX Update Playbook

![Creating Ansible Playbook](screenshots/nginx-report-image-15.png)

The `update_nginx.yml` playbook was created for automated NGINX management.

### 16. Ansible NGINX Patching Playbook

![NGINX Ansible Patching Playbook](screenshots/nginx-report-image-16.png)

The playbook defines tasks for removing the manually installed NGINX and installing the latest available package version.

### 17. Executing the NGINX Patching Playbook

![Ansible Playbook Execution](screenshots/nginx-report-image-17.png)

The Ansible playbook was executed with elevated privileges to automate the NGINX update process.

### 18. Final NGINX Version Verification

![Final NGINX Version Verification](screenshots/nginx-report-image-18.png)

The final verification confirms the updated NGINX installation.

---

### Project Report

The complete technical assessment report is available in:

`report/nginx-security-hardening-report.docx`






## Key Takeaway

The assessment demonstrates the security risks of maintaining an outdated NGINX installation and the value of automated patch management. The documented Ansible workflow helps simplify repetitive administrative tasks, reduce human error, and improve consistency across deployments.
