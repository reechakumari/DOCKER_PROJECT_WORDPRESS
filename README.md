# docker-project
Docker is a computer program that performs operating-system-level virtualization, also known as “containerization”.
This has two main advantages compared to the classic LAMP setup:
*containers are isolated from each other and the communication between them is limited, which increases security
*tools, libraries, config files, and everything the container needs to run is in the container itself, 
which means we’ll have a clean and tidy setup – once we’re done with the container, we can remove it and everything will be gone.

Network driver 
User-defined bridge networks :are best when you need multiple containers to communicate on the same Docker host.
Host networks: are best when the network stack should not be isolated from the Docker host, but you want other aspects of the container to be isolated.
Overlay networks :are best when you need containers running on different Docker hosts to communicate, or when multiple applications work together using swarm services.
Macvlan networks: are best when you are migrating from a VM setup or need your containers to look like physical hosts on your network, each with a unique MAC address.
Third-party network plugins :allow you to integrate Docker with specialized network stacks.


mysql:
SQL stands for Structured Query Language and is the programming language typically used to query databases.
MySQL is a database management system that is used by WordPress to store and retrieve all your blog information

wordpress:
WordPress ( WordPress.org) is a content management system (CMS) based on PHP and MySQL that is usually used with the MySQL or MariaDB database servers but can also use the SQLite database engine.
Features include a plugin architecture and a template system, referred to inside WordPress as Themes.
WordPress requires MySQL to store and retrieve all of its data including post content, user profiles, and custom post types.
WordPress uses the PHP programming language to store and retrieve data from the MySQL database. To retrieve data from the database, WordPress runs SQL queries to dynamically generate content.

Project:
This project include wordpress which uses PHP programming language to store database in mysql database where all data is stored.
I created a docker compose :
"docker-compose" that uses a configuration file to describe all the containers we need, the dependencies they have with each other, and their specific setup
first we have to pull docker compose 
then I created a file as docker_compose.yml 

the file simply defines the two services (or containers, if you will) that we need to run WordPress: mysql and wordpress. 
The former (mysql) contains information about the image we need (which is obviously a MySQL image, version 5.7) and some config parameters. 
The most relevant are probably the port mapping (we’ll be able to access the database using port 8081 in our host, which maps to 3306 in the guest)
and the database setup itself (user, password, and so on).

The latter is WordPress itself (wordpress) and it follows a similar approach. 
Here we tell Docker Compose that we want WordPress to be accessible via the port 8080 in our host. 
We also specify that WordPress relies on the other service: mysql.
And we finally add some additional configuration parameters (essentially, those to access the database).

Once we’re done, save and exit the file

Just wait for a couple of minutes and, once it’s done, go to http://localhost:8080 with your web browser.
you’ll see your new WordPress site.
if we want to create new WordPress instances, you’ll simply have to repeat the steps we’ve discussed. 
That is, you’ll create a new directory in ~/docker/, you’ll add the docker-compose.yml file, and you’ll set it up.
Just make sure that you’re using different ports for this new instance, or you won’t be able to run them both at the same time (for example, use 8082 for WordPress and 8083 for MySQL)

Once you’re done, you can stop the container running the following command:
docker-compose down
as down will not only stop the container, but also remove it completely. 
That is, if you restart a container using docker-compose up after you shut it down using the down command, your WordPress will start from scratch (an empty database, an uninstalled WordPress, etc).

How to check data is stored in mysql or not:
>mysql databases;

>show mysql_storage database;


In this volume all data is stored.

For all this I want to make sure that WordPress and MySQL can talk to each other too, so I have to make sure they’re also in a common network.
 

  
