![](https://github.com/Gonnuru/RealEstate_E2E_ML/blob/master/screenshots/application.jpg)

# Real Estate Price Estimation

> An end to end model of Machine Learning for Real Estate Price Estimation. 

> Deployed on Amazon Ec2 Instance

![GitHub All Releases](https://img.shields.io/github/downloads/Gonnuru/RealEstate_E2E_ML/total?color=%23%2300FF00&logo=GitHub) ![GitHub release (latest by date including pre-releases)](https://img.shields.io/github/v/release/Gonnuru/RealEstate_E2E_ML?include_prereleases) ![GitHub repo size](https://img.shields.io/github/repo-size/Gonnuru/RealEstate_E2E_ML) ![GitHub last commit](https://img.shields.io/github/last-commit/Gonnuru/RealEstate_E2E_ML) [![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)


**Demo**

![Recordit GIF](http://g.recordit.co/P8J3lyqoJU.gif)

## Table of Contents



- [Installation](#installation)
- [Contributing](#contributing)
- [Support](#support)
- [License](#license)


---


## Installation

- All the `code` required to get started can be found at https://github.com/Gonnuru/RealEstate_E2E_ML/blob/master/server/requirements.txt.txt


### Clone

- Clone this repo to your local machine using `https://github.com/Gonnuru/RealEstate_E2E_ML`

### EC2 Setup

1. Create EC2 instance using amazon console, also in security group add a rule to allow HTTP incoming traffic
2. Now connect to your instance using a command like this,
```
ssh -i "Path to Pem File" ubuntu@ec2-3-133-88-210.us-east-2.compute.amazonaws.com
```
3. nginx setup
   1. Install nginx on EC2 instance using these commands,
   ```
   sudo apt-get update
   sudo apt-get install nginx
   ```
   2. Above will install nginx as well as run it. Check status of nginx using
   ```
   sudo service nginx status
   ```
   3. Here are the commands to start/stop/restart nginx
   ```
   sudo service nginx start
   sudo service nginx stop
   sudo service nginx restart
   ```
   4. Now when you load cloud url in browser you will see a message saying "welcome to nginx" This means your nginx is setup and running.
4. Now you need to copy all your code to EC2 instance. You can do this either using git or copy files using winscp. We will use winscp. You can download winscp from here: https://winscp.net/eng/download.php
5. Once you connect to EC2 instance from winscp (instruction in a youtube video), you can now copy all code files into /home/ubuntu/ folder. The full path of your root folder is now: **/home/ubuntu/BangloreHomePrices**
6.  After copying code on EC2 server now we can point nginx to load our property website by default. For below steps,
    1. Create this file /etc/nginx/sites-available/bhp.conf. The file content looks like this,
    ```
    server {
	    listen 80;
            server_name bhp;
            root /home/ubuntu/BangloreHomePrices/client;
            index app.html;
            location /api/ {
                 rewrite ^/api(.*) $1 break;
                 proxy_pass http://127.0.0.1:5000;
            }
    }
    ```
    2. Create symlink for this file in /etc/nginx/sites-enabled by running this command,
    ```
    sudo ln -v -s /etc/nginx/sites-available/bhp.conf
    ```
    3. Remove symlink for default file in /etc/nginx/sites-enabled directory,
    ```
    sudo unlink default
    ```
    4. Restart nginx,
    ```
    sudo service nginx restart
    ```
7. Now install python packages and start flask server
```
sudo apt-get install python3-pip
sudo pip3 install -r /home/ubuntu/BangloreHomePrices/server/requirements.txt
python3 /home/ubuntu/BangloreHomePrices/client/server.py
```
Running last command above will prompt that server is running on port 5000.
8. Now just load your cloud url in browser (for me it was http://ec2-3-133-88-210.us-east-2.compute.amazonaws.com/) and this will be fully functional website running in production cloud environment



---

## Contributing

> To get started...

### Step 1

- **Option 1**
    - 🍴 Fork this repo!

- **Option 2**
    - 👯 Clone this repo to your local machine using `https://github.com/Gonnuru/RealEstate_E2E_ML.git`

### Step 2

- **HACK AWAY!** 🔨🔨🔨

### Step 3

- 🔃 Create a new pull request using <a href="https://github.com/Gonnuru/RealEstate_E2E_ML/compare" target="_blank">`https://github.com/Gonnuru/RealEstate_E2E_ML/compare`</a>.

---


## Support

Reach out to me at 
- Linkedin at <a href="https://www.linkedin.com/in/sampathgonnuru" target="_blank">`Linkedin.com`</a>

---


## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
