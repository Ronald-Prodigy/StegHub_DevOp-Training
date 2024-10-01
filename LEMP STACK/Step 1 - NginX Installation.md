# Step 1 – Installing the Nginx Web Server

In order to display web pages to our site visitors, we are going to employ Nginx, a high-performance web server. We’ll use the `apt` package manager to install this package.

## Update the Package Repositories

Since this is our first time using `apt` for this session, start off by updating your server’s package index:
```bash
$ sudo apt update
```
![apt](<sudo-apt update.png>)

![apt](<still apt -update.png>)

## Install Nginx

Following that, you can use apt install to get Nginx installed:

```bash
$ sudo apt install nginx
```
![nginx](<nginx installation.png>)

When prompted, enter Y to confirm that you want to install Nginx. Once the installation is finished, the Nginx web server will be active and running on your Ubuntu 20.04 server.

### Verify Nginx Installation

To verify that Nginx was successfully installed and is running as a service in Ubuntu, run:

```sh
sudo systemctl status nginx
```
![img](<ngix running.png>)

If it is green and running, then you did everything correctly - you have just launched your first Web Server in the Clouds!

## Open TCP Port 80

Before we can receive any traffic by our Web Server, we need to open TCP port 80, which is the default port that web browsers use to access web pages on the Internet.

As we know, we have TCP port 22 open by default on our EC2 machine to access it via SSH, so we need to add a rule to EC2 configuration to open inbound connection through port 80.

Our server is running and we can access it locally and from the Internet (Source 0.0.0.0/0 means 'from any IP address').

## Test Local Access

First, let us try to check how we can access it locally in our Ubuntu shell. Run:

```sh
curl http://localhost:80
```

or

```sh
curl http://127.0.0.1:80
```

These two commands above actually do pretty much the same - they use the `curl` command to request our Nginx on port 80 (actually you can even try not specifying any port - it will work anyway). The difference is that in the first case we try to access our server via DNS name and in the second one - by IP address (in this case, IP address `127.0.0.1` corresponds to DNS name `localhost`, and the process of converting a DNS name to IP address is called "resolution"). We will touch DNS in further lectures and projects.

As an output, you can see some strangely formatted text. Do not worry; we just made sure that our Nginx web service responds to the `curl` command with some payload.

## Test Internet Access

Now it is time for us to test how our Nginx server can respond to requests from the Internet. Open a web browser of your choice and try to access the following URL:

```vbnet
http://<Public-IP-Address>:80
```
![img](<nginx display page.png>)


