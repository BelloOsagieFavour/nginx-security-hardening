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

Screenshots extracted from the original Word report are stored in the `screenshots/` directory.

The complete project report is stored in:

`report/nginx-security-hardening-report.docx`

## Key Takeaway

The assessment demonstrates the security risks of maintaining an outdated NGINX installation and the value of automated patch management. The documented Ansible workflow helps simplify repetitive administrative tasks, reduce human error, and improve consistency across deployments.
