# web-stack-implementation-lemp-stack-
You have done a great job with successful completion of Project 1.

In this project you will implement a similar stack, but with an alternative Web Server - [NGINX](https://nginx.org/en/), which is also very popular and widely used by many websites in the Internet.

**Side Self Study**
- Make yourself familiar with basic [SQL syntax and most commonly used commands](https://www.w3schools.com/sql/sql_syntax.asp)
-  Be comfortable using not only VIM, but also [Nano editor](https://www.nano-editor.org/) as well, get to know [basic Nano commands](http://www.linuxandubuntu.com/home/nano-cli-text-editor-for-everyone-basic-tutorials)

In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS.

If you do not have an AWS account - go back to [Project 1 Step 0](https://starter-pbl.darey.io/en/latest/project1.html) to sign in to AWS free tier account and create a new EC2 Instance of t2.nano family with Ubuntu Server 20.04 LTS (HVM) image. Remember, you can have multiple EC2 instances, but make sure you STOP the ones you are not working with at the moment to save available free hours.

**Hint:** In previous project we used Putty on Windows to connect to our EC2 Instance, but there is a simpler way that do not require conversion of **.pem** key to **.ppk** - using [Git Bash](https://git-scm.com/downloads).

Download and install Git Bash like it is shown in [this video](https://youtu.be/qdwWe9COT9k).

Launch Git Bash and run following command:

ssh -i <Your-private-key.pem> ubuntu@<EC2-Public-IP-address>

It will look like this:

![](./images/pic1.png)

## installing the nginx web server
In order to display web pages to our site visitors, we are going to employ Nginx, a high-performance web server. We’ll use the **apt** package manager to install this package.

Since this is our first time using **apt** for this session, start off by updating your server’s package index. Following that, you can use **apt install** to get Nginx installed:

- sudo apt update
- sudo apt install nginx

![](./images/pic2.png)

When prompted, enter Y to confirm that you want to install Nginx. Once the installation is finished, the Nginx web server will be active and running on your Ubuntu 20.04 server

To verify that nginx was successfully installed and is running as a service in Ubuntu, run:
- sudo systemctl status nginx

![](./images/pic3.png)

If it is green and running, then you did everything correctly - you have just launched your first Web Server in the Clouds!

Before we can receive any traffic by our Web Server, we need to open [TCP port 80](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers) which is default port that web brousers use to access web pages in the Internet.

As we know, we have TCP port 22 open by default on our EC2 machine to access it via SSH, so we need to add a rule to EC2 configuration to open inbound connection through port 80:

![](./images/GIF1.gif)

Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 means ‘from any IP address’).

First, let us try to check how we can access it locally in our Ubuntu shell, run:
- curl http://localhost:80
- or  curl http://127.0.0.1:80

![](./images/pic4.png)

These 2 commands above actually do pretty much the same - they use ‘curl’ command to request our Nginx on port 80 (actually you can even try to not specify any port - it will work anyway). The difference is that: in the first case we try to access our server via [DNS name](https://en.wikipedia.org/wiki/Domain_Name_System) and in the second one - by IP address (in this case IP address 127.0.0.1 corresponds to DNS name ‘localhost’ and the process of converting a DNS name to IP address is called “resolution”). We will touch DNS in further lectures and projects.

As an output you can see some strangely formatted test, do not worry, we just made sure that our Nginx web service responds to ‘curl’ command with some payload.

Now it is time for us to test how our Nginx server can respond to requests from the Internet. Open a web browser of your choice and try to access following url


