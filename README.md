# 🚀 Support Engineering (TSE) Technical Bootcamp

Welcome to the TSE Bootcamp. This is a self-paced, hands-on program designed to build the "break-fix" and automation skills required for a high-level Technical Support Engineering role.

**The Rule:** There are no tutorials here. You are given **Objectives** and **Goals**. You must use documentation, man pages, logs, and search engines to find the "How." Google it, ask for help, use AI, use whatever tool you can think of to complete these tasks

---

## 🛠 Module 1: Infrastructure & The Foundation

**Objective:** Provision a production-ready Linux environment and establish secure access.

* **Task 1.1:** Deploy a server running **Debian 12** or **Ubuntu 24.04 LTS**. (Proxmox, AWS, or GCP).
* **Task 1.2:** Create a restricted user named `appuser` with `sudo` privileges.
* **Task 1.3:** Generate an **ED25519 SSH keypair** locally. Import it to the server.
* **Task 1.4:** Edit `/etc/ssh/sshd_config` to **disable password-based login** and **disable root SSH login**.

**✅ Goal:** Log in as `appuser` without a password. Prove root login is blocked.

---

## 🔓 Module 2: The "Broken" Service Lab

**Objective:** Diagnose and repair a service installed via a faulty automation script.

* **Task 2.1:** Run the following "Mystery Installer" as root:
```bash
curl -sSL https://raw.githubusercontent.com/HarryV97/-Pocketbase_Install_Bad/refs/heads/main/install.sh | bash

```


* **Task 2.2:** The service will fail. Use `journalctl`, `systemctl status`, and filesystem commands to find the permission and ownership errors.
* **Task 2.3:** Fix the environment manually until the service is running.

**✅ Goal:** `systemctl is-active pocketbase` returns `active`.

---

## 🌐 Module 3: Networking & Reverse Proxy

**Objective:** Secure the server and expose the service on standard web ports.

* **Task 3.1:** Enable `ufw`. Allow SSH (22), HTTP (80), and HTTPS (443). Ensure port `8090` is blocked from the outside.
* **Task 3.2:** Install **Nginx**. Configure a reverse proxy so `https://your-server-ip` points to the internal PocketBase service.
* **Task 3.3:** Generate a self-signed SSL certificate and configure Nginx to use it for port 443.

**✅ Goal:** Access the PocketBase UI in a browser via `https://[IP-ADDRESS]` with no port specified.

---

## 👥 Module 4: The Customer Hand-off

**Objective:** Simulating a live customer environment.

* **Task 4.1:** Access the PocketBase UI and create your admin account.
* **Task 4.2:** Create a collection named `users` with fields: `name` (text), `birthday` (date), and `status` (text).
* **Task 4.3:** Add me (`[YOUR_EMAIL]`) as an admin user. I will then "seed" the database with 2,000 records.

---

## 🧹 Module 5: API Surgery (Data Cleanup)

**Objective:** Use the REST API to perform bulk data manipulation.

* **Task 5.1:** Authenticate with the PocketBase API via `curl` to retrieve an admin token.
* **Task 5.2:** Write a script (Bash or Python) to query the `users` collection.
* **Task 5.3:** Find and **DELETE** every user record where the birthday is in **October 1997**.

**✅ Goal:** Provide a log showing the record count before and after the cleanup.

---

## 📦 Module 6: Containerization (Docker)

**Objective:** Move the service into an isolated container environment.

* **Task 6.1:** Stop the local `systemd` service.
* **Task 6.2:** Deploy PocketBase using **Docker**.
* **Task 6.3:** Ensure **Volume Persistence** is configured. (If the container is deleted/recreated, the data must remain).
* **Task 6.4:** Update the Nginx proxy to point to the new Docker container.

---

## 🪵 Module 7: Ops & Maintenance

**Objective:** Manage system resources and logs.

* **Task 7.1:** Configure `logrotate` for the PocketBase logs to prevent disk exhaustion.
* **Task 7.2:** Find the 500th successful request in the Nginx logs using only `grep`, `awk`, or `cut`.
* **Task 7.3:** Identify and delete a 1GB "junk" file hidden somewhere in `/var` using `du` and `df`.

---

### 💡 Support Lead Note

> "A Support Engineer’s value isn't just in knowing the answer, but in knowing how to find it. If you get stuck, check the logs again. The answer is usually there."
