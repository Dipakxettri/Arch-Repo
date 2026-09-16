# Postgresql Setup

`sudo pacman -S postgresql` -> install

`sudo su - postgres -c "initdb --locale=en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data"` -> Arch Linux does not automatically initialize the database directory. Switch to the postgres user and initialize it

`sudo su - postgres
psql` -> Switch to the postgres system user and open the interactive database shell

`CREATE USER fastapi_user WITH PASSWORD 'your_secure_password';
CREATE DATABASE fastapi_db OWNER fastapi_user;` -> Run the following SQL commands (feel free to change fastapi_user and your password)

`\du
\l
\q` -> Check that your user and database were successfully created, then exit to return to the normal user

# Docker Setup & pgAdmin Cheat Sheet

### 1. Install & Start Docker
* **`sudo pacman -S docker`**
  * *What it does:* Installs the Docker container engine onto your Arch Linux system.
* **`sudo systemctl enable --now docker`**
  * *What it does:* Enables and immediately starts the Docker background service so containers can run.

---

### 2. Run pgAdmin Container
* **`sudo docker run -d --name pgadmin -p 5050:80 \
  -e PGADMIN_DEFAULT_EMAIL=admin@admin.com \
  -e PGADMIN_DEFAULT_PASSWORD=mysecretpassword \
  --add-host=host.docker.internal:host-gateway \
  dpage/pgadmin4`**
  * *What it does:* Downloads (if missing) and runs pgAdmin in the background (`-d`), maps it to port `5050`, sets your login credentials, and uses `--add-host=host.docker.internal:host-gateway` so pgAdmin can talk to your Arch Linux PostgreSQL server.

---

### 3. Verify Container Status
* **`sudo docker ps`**
  * *What it does:* Lists all currently running Docker containers to verify that pgAdmin is active and healthy.

---

### 4. Bypass `sudo` for Docker (Optional, Recommended)
* **`sudo usermod -aG docker $USER`**
  * *What it does:* Adds your user account to the `docker` user group so you don't need root permissions.
* **`newgrp docker`**
  * *What it does:* Refreshes your current terminal session group permissions immediately without requiring a full log out.
* **`docker ps` (Verification)**
  * *What it does:* Tests running Docker commands without `sudo` to ensure permissions are applied correctly.


daily workflow 
`sudo systemctl start postgresql`
`dockor start pgadmin`


stores data at here:
`sudo ls -l /var/lib/postgres/data/`

