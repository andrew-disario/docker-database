<h1>Docker Database</h1>
<p align="center">
<img src="https://github.com/andrew-disario/docker-database/blob/main/docker_mysqlworkbench_logos.png?raw=true" height="75%" width="75%" alt="docker_mysqlworkbench"/>
<br />
In this project, we set up and run a database using Docker and MySQL Workbench. Docker is an open platform for developing, shipping, and running applications and MySQL Workbench is a unified visual tool for database architects, developers, and DBAs that provides data modeling, SQL development, and comprehensive administration tools for server configuration, user administration, backup, and much more. 
<h2>Part 1 - Set Up Docker</h2>

<b> Download and Install Docker </b>
1. Go to [docker.com](https://www.docker.com/) and select **"Get Started"**
2. Select **"Docker Desktop"** and choose the right version for your machine
3. Install Docker when the download finishes

<b> Create Docker Hub Account </b>
1. Go to [hub.docker.com](https://www.hub.docker.com/) and select **"Sign Up"**
2. Enter your information, choose a plan and verify your email address

<h2>Part 2 - Download MySQL Image and Run Docker</h2>

<b> Download and Install Docker </b>
1. Go to [hub.docker.com](https://www.hub.docker.com/), search for "mysql" and select the **"mysql"** result
2. Copy the command from the **"How to use this image"** section
   - ***docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag***

<b> Understand the Docker Run Command </b>
- ***docker run*** :: Runs a command in a new container, pulling the image if needed
- ***--name some-mysql*** :: Names the image "some-mysql"
- ***-e*** :: Refers to environment variables
  - ***MYSQL_ROOT_PASSWORD=my-secret-pw*** :: Sets root password to "my-secret-pw"
- ***-d*** :: Activates detached mode
- ***mysql*** :: Paths to image on docker hub
  - ***:tag*** :: Specifies version "tag"
 
<b> Adjust the Docker Command </b>
1. Replace ***some-mysql*** with your own image name (optional)
2. Replace ***my-secret-pw*** with your own password (optional)
3. Remove ***:tag*** to download latest version of MySQL image
4. Add ***-p 3306:3306*** to open the port from the docker container
- ***docker run --name mysql-image -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql***

<b> Log In to Docker and Download Image to Docker </b>
1. Open terminal and run command: ***docker login***
2. Enter Docker Hub username and password
3. Run command:
***docker run --name mysql-image -p 3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql***
    - This can take a few minutes to run
    - When it finishes the image will start up
    - Will result in an error if the image name already exists
5. Run command: ***docker ps*** to check image status
   - Shows a list of all images that are running
   - Statuses include Starting, Healthy, Up in X seconds, Etc.
  
<h2>Part 3 - Connect MySQL Workbench and Set Up Database </h2>

<b> Connect Using MySQL Workbench </b>
1. Select **"Create a New Connection"** and enter connection details (available at [Docker Hub - mysql](https://hub.docker.com/_/mysql)):
    - Enter Connection Name: ***Local Docker***
    - Enter Hostname: ***Local Host***
    - Enter port: ***3306***
    - Enter Username: ***root***
    - Enter Password: ***my-secret-pw*** (or whatever password you chose)
2. Select **"Test Connection"** to confirm connection
3. Select **"Ok"**

<b> Set Up Database and Query Data</b>
1. Open the SQL Editor
2. Run the SQL queries below one at a time:
    - ***CREATE DATABASE db;***
    - ***USE db;***
    - ***CREATE TABLE employees(id int not null, name text, primary key (id));***
    - ***INSERT INTO employees (id, name) values (1, 'Baker'), (2, 'Jackson'), (3, 'Maxwell');***
    - ***SELECT * FROM db.employees;***
3. Run command: ***docker stop mysql-image*** to stop the Docker image when finished
    - This can also be done using the interface in Docker Desktop

