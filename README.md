# AGAMal Ansible – Update & Secure Ubuntu

This playbook **automates security patching** for Ubuntu 20.04/22.04 servers at AngloGold Ashanti Malaria Control (AGAMal).  
It refreshes the APT cache, performs a **full dist‑upgrade**, enables *unattended‑upgrades* for future CVE fixes, and reboots only when the kernel changes.
