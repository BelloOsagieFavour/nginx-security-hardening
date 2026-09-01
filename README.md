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

The following evidence documents the deployment, vulnerability assessment, and automated patching of the NGINX server.

### 1. Kali Archive Key Configuration

![Kali Archive Key Configuration](screenshots/nginx-report-image-1.png)

The Kali archive key was downloaded and configured to support trusted package installation.

### 2. SSH Service Installation and Verification

![SSH Service Configuration](screenshots/nginx-report-image-2.png)

The OpenSSH service was installed, started, enabled, and its status was verified.

### 3. Downloading NGINX 1.15.5

![Downloading NGINX 1.15.5](screenshots/nginx-report-image-3.png)

The outdated NGINX 1.15.5 source archive was downloaded for the security assessment.

### 4. Installing NGINX Dependencies

![Installing NGINX Dependencies](screenshots/nginx-report-image-4.png)

Required build dependencies were installed before compiling NGINX from source.

### 5. Extracting the NGINX Source

![Extracting NGINX Source](screenshots/nginx-report-image-5.png)

The NGINX 1.15.5 source archive was extracted.

### 6. Configuring and Compiling NGINX

![Configuring and Compiling NGINX](screenshots/nginx-report-image-6.png)

The NGINX source was configured and the installation process was initiated using `make install`.

### 7. Starting the NGINX Server

![Starting NGINX](screenshots/nginx-report-image-7.png)

The manually compiled NGINX server was started using the NGINX binary.

### 8. NGINX Configuration Validation

![NGINX Configuration Test](screenshots/nginx-report-image-8.png)

The NGINX configuration was tested using `nginx -t` and reported successful configuration syntax.

### 9. Initial NGINX Version Verification

![Initial NGINX Version](screenshots/nginx-report-image-9.png)

The initial installation was verified as NGINX 1.15.5, establishing the outdated baseline.

### 10. Nessus Vulnerability Findings — NGINX

![Nessus NGINX Findings](screenshots/nginx-report-image-10.png)

Nessus vulnerability scan results showing security findings associated with the NGINX environment.

### 11. Nessus Vulnerability Findings — ImageMagick

![Nessus ImageMagick Findings](screenshots/nginx-report-image-11.png)

Additional vulnerability findings identified by Nessus for ImageMagick and related components.

### 12. Nessus Vulnerability Findings — SSL/TLS

![Nessus SSL TLS Findings](screenshots/nginx-report-image-12.png)

Nessus findings related to SSL/TLS security configuration.

### 13. Installing Ansible

![Installing Ansible](screenshots/nginx-report-image-13.png)

Ansible was installed to automate the NGINX patching process.

### 14. Verifying Ansible Installation

![Ansible Version Verification](screenshots/nginx-report-image-14.png)

The Ansible installation was verified and the installed version was displayed.

### 15. Creating the NGINX Update Playbook

![Creating update_nginx.yml](screenshots/nginx-report-image-15.png)

The `update_nginx.yml` file was created to automate the NGINX update process.

### 16. Ansible NGINX Patching Playbook

![NGINX Ansible Patching Playbook](screenshots/nginx-report-image-16.png)

The playbook defines tasks for removing the manually installed NGINX, updating packages, installing NGINX, and managing the NGINX service.

### 17. Executing the Ansible Playbook

![Ansible Playbook Execution](screenshots/nginx-report-image-17.png)

The Ansible playbook was executed with elevated privileges and the task results were displayed.

### 18. Final NGINX Version Verification

![Final NGINX Version](screenshots/nginx-report-image-18.png)

The final verification shows that NGINX was successfully updated to version 1.30.1.

---

### Project Report

The complete technical assessment report is available in:

`report/nginx-security-hardening-report.docx`

### Project Report

The complete technical assessment report is available in:

`report/nginx-security-hardening-report.docx`






## Key Takeaway

The assessment demonstrates the security risks of maintaining an outdated NGINX installation and the value of automated patch management. The documented Ansible workflow helps simplify repetitive administrative tasks, reduce human error, and improve consistency across deployments.
