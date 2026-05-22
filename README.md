# DevOps Home Lab: GitLab CI/CD

This project is a DevOps practice lab focused on implementing a robust CI/CD pipeline using a self-hosted GitLab instance. The goal was to bridge the gap between theoretical knowledge and practical infrastructure management.

## 🚀 Project Overview
The objective was to build a fully automated CI/CD pipeline for a static website (built with Hugo). By self-hosting the infrastructure, I gained hands-on experience with service configuration, runner orchestration, and containerized deployment.

## 🛠 Tech Stack
- **Version Control:** Git & GitLab (Self-Hosted)
- **Infrastructure:** Docker & Docker Compose
- **CI/CD:** GitLab CI (Runners, Pipelines, Stages)
- **Web Framework:** Hugo

---

## 💡 What I Learned
### 1. GitLab & Infrastructure
- **Self-Hosted GitLab:** I set up a self-hosted instance to understand the underlying architecture, specifically how GitLab interacts with the file system and external services.
- **GitLab Runners:** Learned how to configure and register runners to execute CI jobs. Understanding how these runners interact with the Docker daemon was a key takeaway for troubleshooting production environments.

### 2. CI/CD Implementation
- **Pipeline Architecture:** Built multi-stage pipelines (Build, Test, Deploy) to manage the application lifecycle.
- **Artifact Management:** Learned to pass data between stages using GitLab artifacts to maintain efficiency.
- **Environment Variables:** Implemented secure management of project-level variables for configuration and sensitive data.

### 3. Containerization
- **Dockerfiles:** Refined my knowledge of container optimization, specifically implementing `ENTRYPOINT` vs. `CMD` to handle container initialization effectively.
- **Docker Compose:** Utilized Compose to orchestrate multi-container environments, ensuring that the development and production configurations remained consistent.

### 4. Git & Workflow
- Strengthened my understanding of Git through hands-on use of `git revert` for safe change reversal, `git stash` for temporary work preservation, and **submodules** for managing external dependencies.

### 5. Static Site Generation (Hugo)
- Integrated Hugo as a lightweight, performant tool for site generation. This experience provided me with a reliable workflow for deploying documentation or technical blogs in the future.

---

## 🏗 Setup & Usage

### Prerequisite
- The target webserver must have ssh-server and rsync installed.
- The deploy path in the target webserver must have proper permissions so that the deploy user can write in it. 

_(Tip: Add a small section here on how to run it. Even a simple `docker-compose up` command shows you value reproducibility.)_
1. **Clone the repository** 
```bash
git clone https://github.com/FaridG7/DevOps_Home_Lab-GitLab-CICD.git
cd DevOps_Home_Lab-GitLab-CICD
```

2. **Start the environment** (if you want to use my infrastructure otherwise start your own environment)
	refer to the [infrastructure's guide](https://github.com/FaridG7/DevOps_Home_Lab-GitLab_CICD-Infrastructure#getting-started)

3. **Generate a private key without a passphrase**
```bash
ssh-keygen -f /ssh-key -N ""
```
*don't worry, ssh-key directory is ignored by git and won't go into the remote repository*

4. **Add the key to the target webser's authorized_keys**
```bash
ssh-copy-id <deploy user>@<target hostname>
```

5. **Add the (private) key to the project as a project variable file**
	1. Go to the project in Gitlab. 
	2. Go to the Settings > CI/CD. 
	3. Expand Variables. 
	4. Add a variable. 
	5. Set the variable type to file, set key to `SSH_PRIVATE_KEY_FILE` and paste the key in the value section.
	6. Click add

6. Voila! Now all you're commits on main branch are automatically deployed on the target.

---

## 📈 Future Improvements

- [ ] Establish a clean git workflow
- [ ] Use version-like deployment (so that improper rsyncing doesn't break the website)
- [ ] Integrate a reverse proxy (like Nginx Proxy Manager) to handle SSL/TLS.
- [ ] Adding a secret management vault
