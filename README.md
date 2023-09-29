# project-4

## CLIENT SERVER ARCHITECTURE WITH MYSQL AS RDBMS

The aim of this project is to explore the intricacies of client-server architecture using MYSQL as the RDBMS.

Two Linux-based virtual servers (EC2 instances in AWS) were created and configured. One server is named mysql_server and the other server was named mysql_client.

The following commands was run to install mysql-server on the mysql_server 

**`sudo apt update`**
**`sudo apt install mysql-server`**

The following command was used to log in to the MySQL console

**`sudo mysql`**

A root user password was set using mysql_native_password as default authentication method.

**`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'kalkah';`**

I exit the MySQL console to start MYSQL interactive script using the command below. This remove some insecure default settings and lock down access to the database system. This script also prompt me to configure the validate password plugin.

**`sudo mysql_secure_installation`**

<img width="443" alt="image" src="https://github.com/kalkah/project-4/assets/95209274/b954fca1-f6ed-4a70-b9ea-e54319480a9d">

remote_user was created with the command below, 

**`CREATE USER name 'remote_user'@'%', IDENTIFIED WITH mysql_native_password BY 'kalkah'`;** (% here means that any IP address can be use by the remote_user and the user should be identified with mysql native password)

Create the database name 'test_db' with the command **`CREATE DATABASE test_db;`**

Granted all privileges on the database name "test_db" to remote user using the command below:

**`GRANT ALL ON test_db.* TO 'remote_user'@'%' WITH GRANT OPTION;`**

Flush the priviledges - **`FLUSH PRIVILEGES`**

The following commands was run to install mysql-client on the mysql_client server

**`sudo apt update`**
**`sudo apt install mysql-client`**

To allow remote connection to the mysql-server, port 3306 was opened in the inbound rules of mysql-server.

<img width="710" alt="image" src="https://github.com/kalkah/project-4/assets/95209274/cb205a33-34a3-46fd-84ca-a85e161a99a8">

On the mysql-server, mysqld.cnf was edited to allow connections from remote host using the command below.

**`sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`**

set the binding address to 0.0.0.0

<img width="559" alt="image" src="https://github.com/kalkah/project-4/assets/95209274/92e627a5-6e13-4f4e-ae49-7b17d60e1981">

I use **`sudo systemctl restart mysql`** command to restart mysql server

From the client_server, I remotely connect to the mysql-server using the command below
**`sudo mysql -u remote_user -h 172.31.89.59 -p`**

<img width="443" alt="image" src="https://github.com/kalkah/project-4/assets/95209274/afae2824-7f2d-466a-ab5b-cea3a749577a">

The command **`show databases;`** was run to show that I can interract with the database.

<img width="453" alt="image" src="https://github.com/kalkah/project-4/assets/95209274/64be7ee8-5cc5-4c63-8746-f670bd980638">


