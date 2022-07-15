# Listmonk-installing-process

## Step 1 — Get the file

Clone the fils from github. Listmonk Repository :- https://github.com/knadh/listmonk/ . Or get the latest source code using wget.

Type: 
          git clone https://github.com/knadh/listmonk.git  
          
OR
Type : 

          sudo yum install wget 
          cd /opt
          wget "https://github.com/knadh/listmonk/archive/refs/tags/v2.1.0.tar.gz"

You can also use other package manager like aptitude, dnf, yay etc.


## Step 2 — Prepare the Environment

Type: 

          sudo yum update # Update your system
          sudo yum upgrade #Upgrade your system
          sudo yum install docker docker-compose  # Install docker & docker-compose

On Ubuntu : 

Type : 

          sudo apt install wget ca-certificates #  For a secure SSL connection
          sudo apt update # Update your system
          sudo apt upgrade #Upgrade your system
          sudo apt install docker docker-compose  # Install docker & docker-compose
          sudo apt install postgresql postgresql-contrib  # Install postgresql and dependencies

For Ubuntu less that 20 version may need these commands:

Type :

          wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -  # Add postgresql key
          sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'  
          sudo apt update # Update your system again
          sudo apt install postgresql postgresql-contrib  # Install postgresql and dependencies


## Step 3 — Fix the future bug

In Cent OS you may have some experience of getting error on docker-compose version or environment variable and path. Now we are gonna fix variable problem which is very much common,

Type : 

          sudo groupadd docker # add group docker
          sudo gpasswd -a username docker # add user docker

If you still face Error of docker-compose version follow these command.

Type: 

          sudo yum insall curl
          cd /opt
          sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
          sudo chmod +x /usr/local/bin/docker-compose

Then Simple restart docker service.

Type : 
          sudo service docker restart
          docker–compose –-version # Check docker version


## Step 4 — Go for production

Extract the tar folder:
Type: tar xvf v2.1.0.tar.gz

If you clone the repository 7 & already extract the tar folder the enter the directory of listmonk using for automation system:-

Type :

          cd listmonk
          sudo chmod +x install-prod.sh
          ./install-prod.sh  # run listmonk on http://localhost:9000 with user listmonk & password listmonk

For manual setup: 
          
## Step 5 — Edit the config

Type: 

          nano docker-compose.yml

Edit the Environment section like following on line 24-26:

 environment:
 
    - POSTGRES_PASSWORD=listmonk
    - POSTGRES_USER=listmonk
    - POSTGRES_DB=listmonk
    

You can also edit port on line 11 and container name on line 37 for service and 45 for app.

Then copy config.toml and edit it with the same details as docker-compose.yml. on my terms as I changed password which is under db section in config.toml on 20.

Type : 
          cp config.toml.sample config.toml
          nano config.toml

Example: 

          user = "listmonk"
          password = "listmonk"
          database = "listmonk"

If you change port change it also on config.toml on line 6 and host on 17.

Run your server.

Type : 
          docker-compose up app 

Get listmonk on:

          http://localhost:9000
