# Odoo Example

####
### Local Testing with Docker

**Build**
```sh
docker build -t klovercloud/odoo:13.0 .
```

**Run Postgres**
```sh
docker run -d -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres --name db postgres:10
```

**Run Odoo**
```sh
docker run -p 8069:8069 --name odoo --link db:db --read-only --tmpfs=/tmp -v /Users/whyxn/docker-vol/odoo/addon:/mnt/extra-addons -v /Users/whyxn/docker-vol/odoo/data:/var/lib/odoo whyxn/odoo:13.0
```

####
### Run in KloverCloud
**Database**
- Create a Postgres Server with a PgAdmin
- Connect to your Postgres Server via PgAdmin and create a user for odoo having the priviledge to create databases
- Do not create any database for odoo
####
**Application**
- On-board this repository as Application
- Assign minimum 1vCPU and 2.75GB RAM
- Persistent Volume is required (Min 10 GB)
- The following paths should be in the Volume Mount paths
```
/var/lib/odoo
/mnt/extra-addons
```
- Create Application
- Set Environment Variables / Secrets to provide configurations for PostgreSQL
```
HOST=<YOUR_POSTGRES_ENDPOINT>
USER=<YOUR_POSTGRES_ODOO_USERNAME>
PASSWORD=<YOUR_POSTGRES_ODOO_PASSWORD>
```
- Deploy Odoo