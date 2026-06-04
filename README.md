# WordPress with Docker Compose

A fully containerised WordPress deployment using Docker Compose.
Built as part of my Cloud & DevOps learning journey.

## Stack

| Service   | Image                  | Role                        |
|-----------|------------------------|-----------------------------|
| webserver | nginx:latest           | Web server / reverse proxy  |
| wordpress | wordpress:php8.2-fpm   | PHP application + PHP-FPM   |
| db        | mariadb:11             | Database                    |

## Project Structure
```
project12-wordpress/
├── docker-compose.yml
├── .env                  ← credentials (not committed)
├── .gitignore
└── nginx-conf/
└── nginx.conf
```
## How to Run

**1. Clone the repo**
```bash
git clone https://github.com/haseebspaniard/wordpress-docker-compose.git
cd wordpress-docker-compose
```

**2. Create your .env file**
```bash
cp .env.example .env
# Edit .env and set your own passwords
```

**3. Start all containers**
```bash
docker compose up -d
```

**4. Open in browser**
http://localhost
**5. Complete WordPress setup through the web interface**

## Architecture
Browser
↓ HTTP (port 80)
Nginx Container
↓ FastCGI (port 9000)
WordPress + PHP-FPM Container
↓ SQL (port 3306)
MariaDB Container
All three containers communicate over a custom Docker bridge
network called app-network. Only port 80 is exposed externally.

## Key Commands

```bash
docker compose up -d        # Start all containers
docker compose ps           # Check container status
docker compose down         # Stop containers (data safe)
docker compose logs <name>  # View container logs
docker exec -it db mariadb -u root -p   # Enter database
```

## Volumes

| Volume    | Mounted At          | Purpose                  |
|-----------|---------------------|--------------------------|
| wordpress | /var/www/html       | WordPress files          |
| dbdata    | /var/lib/mysql      | MariaDB data             |

Data persists across container restarts via named volumes.

## Author

Abdul Haseeb — former CS teacher transitioning into Cloud & DevOps.

- Medium: https://medium.com/@haseebabdul480
- LinkedIn: https://www.linkedin.com/in/abdulhaseebas
- GitHub: https://github.com/haseebspaniard
