# Set up a PostgreSQL server and pgAdmin with Docker Linux OS
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
NOTE: curl may not be installed on your Linux distribution. If that’s the case, you can install curl with the following command:
# Ubuntu/Debian/Linux Mint:
```
sudo apt install curl -y
```
# CentOS/RHEL/Fedora:
```
sudo dnf install curl -y
```
Once docker-compose binary file is downloaded, run the following command:
```
sudo chmod +x /usr/local/bin/docker-compose
```
# Setting Up Docker Compose for the Project:
Now, create a project directory (let’s say ~/docker/pgdev) as follows:
```
mkdir -p ~/docker/pgdev
```
Now, navigate to the project directory ~/docker/pgdev as follows:
```
cd ~/docker/pgdev
```
Now, create a **docker-compose.yaml** file in the project directory _~/docker/pgdev_ and type in the following lines in the **docker-compose.yaml** file.
**The docker-compose.yaml** file should look as follows.
```
version: "3.7"
services:
  db:
    image: postgres:12.2
    restart: always
    environment:
        POSTGRES_DB: postgres
        POSTGRES_USER: admin
        POSTGRES_PASSWORD: secret
        PGDATA: /var/lib/postgresql/data
    volumes:
      - db-data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
 
  pgadmin:
    image: dpage/pgadmin4:4.18
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: muhammadalihakimov03@gmail.com
      PGADMIN_DEFAULT_PASSWORD: secret
      PGADMIN_LISTEN_PORT: 80
    ports:
      - "8080:80"
    volumes:
      - pgadmin-data:/var/lib/pgadmin
    links:
      - "db:pgsql-server"
volumes:
  db-data:
  pgadmin-data:
```
* Install docker 
```
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker --now
docker
```
# Starting PostgreSQL server and pgAdmin:
Now, to start the db and pgadmin services, run the following command:
```
docker-compose up -d
```
After commands in terminal
```
Status: Downloaded newer image for dpage/pgadmin4:4.18
Creating pgdev_db_1 ... done
Creating pgdev_pgadmin_1 ... done
```
As you can see, the port 8080 and 5432 are opened by the docker-proxy service.
```
sudo netstat -tlpn
```
To see how the ports are mapped, run the following command:
```
docker-compose ps
```
As you can see, for the db service, the Docker host port 5432 is mapped to the container TCP port 5432.

For the pgadmin service, the Docker host port 8080 is mapped to the container TCP port 80.
Accessing pgAdmin from Web Browser:
# Now, you can easily access pgAdmin 4 from your web browser.

Visit http://localhost:8080 from your Docker host or http://192.168.20.160:8080 from any computer on your network. You should see the pgAdmin login page. Login with your email and password.

