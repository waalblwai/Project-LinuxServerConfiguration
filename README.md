Project: Linux Server Configuration


The finla project of Full Stak Web Developer Nanodegree. I was asked to insatll a Linux server and prepare it to host my web application of previous project "Item Catalog". 


Link to my previous Project: FragranceShop

Server Info:


URL: http://34.208.30.71.xip.io
IP: 34.208.30.71
Port: 2200
IP: 34.208.30.71


GRADER:

SSH passphrase: no passphrase
user password: 123

Getting Started:
This project uses Amazon Lightsail to create a Linux server instance.

    1.Get your server.

        * Start a new Ubuntu Linux server instance on Amazon Lightsail.
            - Log in!
            - Create an instance
            - Choose an instance image: Ubuntu (OS only)
            - Choose your instance plan (lowest tier is fine)
            - Give your instance a hostname
            - Wait for startup
            - Once the instance has started up, follow the instructions provided to SSH into your server.

    2. Secure your server. (On the Amazon lightsail)
        * Update all currently installed packages.

        sudo apt-get update
        sudo apt-get upgrade

    3. Change SSH port to 2200: using this command, and going to the line where it says Port 20, change to 2200

        sudo nano /etc/ssh/sshd_config


    4.Configure Firewall Using the command belw.

        sudo ufw allow www
        sudo ufw allow 123/udp
        sudo ufw allow 2200


    5. Create grader user

        sudo adduser grader

    6. Give grader Sudo

        sudo usermod -aG sudo grader


    7. Create an SSH Create ssh key in the local machine using

        ssh-keygen
    Then go back to the server to switch to grader user using;

        su -u grader
        add .ssh and .ssh/authorized_keys file

        mkdir /.ssh/
        nano /.ssh/authorized_keys   # copy the key here
        
        You can now connect using the command:

        $ ssh -i /grader grader@34.208.30.71 -p 2200

    8. Setup Python3 Environment:
        - First, update apt-get.
            sudo apt-get update
        - Python3 (3.5 at the time of writing) should be already available on EC2 but pip still needs to be installed.
            sudo apt-get install python3-pip
        - Get virtualenv.
            pip3 install virtualenv
        - Create the project folder or clone the project from your Git repository.
            mkdir flaskproject
        - Set up the virtual environment.
            cd flaskproject
            virtualenv venv
        - Activate the environment (use deactivate to exit the environment).
            . venv/bin/activate

    9. Configure the local timezone to UTC.

        sudo dpkg-reconfigure tzdata


    10. Install apache

        sudo apt-get install apache2
        sudo apt-get install libapache2-mod-wsgi-py3
    
    11. Install postgreSQL

        sudo apt install postgresql
        - Create the database and give permission:

            CREATE USER FRAG;
            ALTER USER FRAG CREATEDB;
            CREATE DATABASE FRAG_CATALOG WITH OWNER FRAG;

    12- Install Git

        sudo apt-get install git

    13- Clone the project

        sudo git clone https://github.com/waalblwai/FragranceShop.git catalog

        - install all libraries and requirements:

            sudo pip3 install flask
            sudo pip3 install oauth2client
            sudo pip3 install requests
            sudo pip3 install sqlalchemy
            
    14- WSGI Application edit the file

        sudo nano /etc/apache2/sites-available/000-default.conf

    15. Restart to launch

        sudo service apache2 restart
        


Resources:

    - https://medium.com/@mariasurmenok/creating-a-server-with-amazon-lightsail-11c377cf814c
    - https://vishnut.me/blog/ec2-flask-apache-setup.html
    - http://flask.pocoo.org/docs/0.12/deploying/mod_wsgi/
    - https://askubuntu.com/questions/138423/how-do-i-change-my-timezone-to-utc-gmt
    - https://websiteforstudents.com/how-to-disable-remote-logon-for-root-on-ubuntu-16-04-lts-servers/
    - http://httpd.apache.org/docs/current/mod/mod_alias.html#alias
    - https://linuxacademy.com/blog/linux/linux-commands-for-beginners-sudo/
    - https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/
