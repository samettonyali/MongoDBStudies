# MongoDBStudies
MongoDB Installation and Sample Projects

This project explains how MongoDB is installed on Ubuntu 18.04 LTS and includes some MongoDB projects to explain how it is accessed over applications (Web or Desktop).

## Step 1 - MongoDB Installation on Ubuntu 18.04 LTS

### Prerequisites

You may be required to import the software distributor's GPG keys to ensure the consistency and authenticity of the package. Execute this command to import MongoDB keys to your server.

<code><b>$</b> sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 68818C72E52529D4</code>

Create a MongoDB list file in <i>/etc/apt/sources.list.d/</i> by executing this command

<code><b>$</b> sudo echo "deb http://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list</code>

### Installation

Update the repository...

<code><b>$</b> sudo apt update</code>

and install MongoDB

<code><b>$</b> sudo apt install -y mongodb</code>

You can verify its status by running the command shown below

<code><b>$</b> sudo systemctl status mongodb</code>

Or you can see that it has been started listening on port 27017 with the netstat command below

<code><b>$</b> sudo netstat -plntu</code>

## Step 2 - MongoDB Service Management

As soon as MongoDB is installed it starts running. In order to stop, start, restart, disable, or enable it you should execute these service commands, respectively.

<code><b>$</b> sudo systemctl stop mongodb</code>

<code><b>$</b> sudo systemctl start mongodb</code>

<code><b>$</b> sudo systemctl restart mongodb</code>

<code><b>$</b> sudo systemctl disable mongodb</code>

<code><b>$</b> sudo systemctl enable mongodb</code>

## Step 3 - Remote Access on Firewall

MongoDB runs on port 27017 by default. However, enabling access to MongoDB from everywhere gives unrestricted access to the database data, which is a security threat for applications. Therefore, we need to give access to specific IP address location to default MongoDB's port by executing following command.

<code><b>$</b> sudo ufw allow from <i>yourServerIP</i>/32 to any port 27017</code>

<code><b>$</b> sudo ufw status</code>

If the firewall is inactive it can be enabled by executing the following command.

<code><b>$</b> sudo ufw enable</code>

Also, you need to add your server IP address to <i>/etc/mongodb.conf</i> configuration file as shown below

<code>bind_ip = 127.0.0.1,<i>yourServerIP</i></code>

#port = 27017

After the modification and exiting the editor you should restart MongoDB.

<code><b>$</b> sudo systemctl restart mongodb</code>

## Step 4 - Creating MongoDB Credentials

