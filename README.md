---
title: "Problem And Resolve for learn shell scripting "
ouput : pdf_document
---


# Learn Shell Scripting

## PROBLEM AND SOLVING

1. __when clonning git use HTTPS__

    1. Problem

        > *_NOTES:_* when cloning git in ubuntu not simply in windows

    2. solving
        ```
         git clone https://[user]:token@link_reposity
         ```

        > for easy way in your linux ,, make sure you made invorentment variable for username and your token


2. __when cloning git use SSH__


    * Step 1 Check For Existing SSH Keys 


        ```
        $> ls -al ~/.ssh
        ```

        Do you see any files named id_rsa and id_rsa.pub?

        If yes go to Step 3

        > *_Notes_* : If no, you need to generate them

        <br />

    * Step 2 Generate a new SSH Key

        ```
        $> ssh-keygen -t rsa -b 4096 -C "Your Email" -f ~/.ssh/id_rsa -P ""
        ```

        and your SSH key to the ssh-agent

        ```
        $> eval "$(ssh-agent -s)"
        ```

        ```
        $> ssh-add ~/.ssh/id_rsa
        ```

        <br />

    * Step 3.1 Add the SSH key to your GIT account
    Get Your public key 

        ```
        $> cat ~/.ssh/id_rsa.pub
        ```

        go to your GIT project -> Settings -> SSH Keys

        Then paste the content of your public key in SSH keys

        <br />

    *  Step 3.2 Force SSH Client To use Given Private Key
        <br/>

        *_Notes_* : this is an alternative solution when you can't set keys on your GIT account

        <br />
        ```
        $> sudo nano ~/.ssh/config
        ```

        Then change this line

        IdentityFile < yourPrivateKey >

        <br />
    * Step 4 Clone your Project Repository

        ```
        git clone git@github.com:$USERNAME/$REPONAME.git
        ```

        and if you want to test your SSH is success connecting or not, then following this command

        ```
        ssh -T git@github.com
        ```
        [more info](https://help.github.com/articles/testing-your-ssh-connection/ "Setting ssh connection in github")

3. Problem when issue write export PATH

    at the time my friend test laravel in ubuntu OS,, after setting variable environtment PATH and then he failure writte PATH and become error for ubuntu system and not loggin with KDE.

    <br />

    1. __Problem__
    this warning when command shell apt or anything become error for console.

    ```
    bash: export `=` not a valid identifier
    ```

    2. __Solving__

        > if your position has logged in , go to step 2
        * step 1
            a. hold <kbd> Ctrl </kbd> + <kbd>ALT</kbd> + <kbd>F5</kbd> 

            b. and then your login user your username and your password

        * step 2 
            because my friend failure when create PATH in ~/.bashrc then following this command :
            ```
            sudo nano ~/.bashrc
            ```

            after open content file .bashrc , Delete PATH which failure and hold <kbd>Alt</kbd> + <kbd>X</kbd> And hold<kbd>Y</kbd>

        * Step 3
            ```
                sudo systemctl reboot
            ```

        <br/>
4. when you forgot password mariadb or mysql, you should reset.

    * Step 1
        stop service your mysql
        ```
            sudo systemctl stop mysql
        ```
        or
        ```
            sudo service mysql stop
        ```
        or in ubutnu & debian
        ```
            sudo /etc/init.d/mysql stop
        ```
        or for other distribution versions on CentOS, Fendora and RHEL
        ``` 
            sudo /etc/init.d/mysqld stop
        ```

    * Step 2
        
        start mysql in safe mode

        ```
        sudo mysqld_safe --skip-grant-tables &
        ```

    * Step 3
        Login into MYSQL using root

        ```
        mysql -u root;
        ```

    * Step 4
        Select the MYSQL database to use

        ```
        use mysql
        ```

    * Step 5

        Reset or change the password user root

        5.1 MYSQL version < 5.7

        ```
        update user set password=PASSWORD("newpassword") where user='root';
        ```

        5.2 MYSQL 5.7 or other than , mysql.user table "password" field -> "authentication_string"

        ```
        update user set authentication_string=password("newpassword") where user='root'; 
        ```

    * Step 6

        Flush the privileges, this function for reread without restarting mysql server

        ```
        flush privileges;
        ```

    * Step 7
        Quit to mysql

        ```
        quit
        ```

    * Step 8
        Stop and start the server again

        8.1 For Ubuntu & Debian

        ```
        sudo /etc/init.d/mysql stop
        sudo /etc/init.d/mysql start
        ```
       
        8.2 For CentOS, Fendora, and RHEL

        ```
        sudo /etc/init.d/mysqld stop
        sudo /etc/init.d/mysqld start
        ```

    * Step 9
        Login With a new password

        ```
        mysql -u root -p
        ```

    * Step 10
        Type the new password and enjoy your server again like nothing happend
       
5. if you want to create another user for access mariadb

    * Step 1

        Login to Mysql using root

        ```
        mariadb -u root -p
        ```
        make sure your typing correct password 

    * Step 2
        create new user 

        ```
        GRANT ALL ON *.* TO 'newuser'@'host/localhost' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;
        ```

    * Step 3
        flush privileges for recheck all without restarting mysql server


        ```
        flush privileges
        ```

    * Step 4
    
        ```
        quit
        ```

    * Step 5
        When installed from the default repositories, MariaDB will start running automatically. To test this, check its status.

            ```
            sudo systemctl status mariadb
            ```

        then , You’ll receive output that is similar to the following:
            ```

            Output :

            ● mariadb.service - MariaDB 10.3.22 database server
            Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: enabled)
            Active: active (running) since Tue 2020-05-12 13:38:18 UTC; 3min 55s ago
            Docs: man:mysqld(8)
                    https://mariadb.com/kb/en/library/systemd/
            Main PID: 25914 (mysqld)
                Status: "Taking your SQL requests now..."
                Tasks: 31 (limit: 2345)
                Memory: 65.6M
                CGroup: /system.slice/mariadb.service
                        └─25914 /usr/sbin/mysqld
                ```

        If MariaDB isn’t running, you can start it with the command 

        ```
        sudo systemctl start mariadb.
        ```

    <br/>
    * Step 6

    For an additional check, you can try connecting to the database using the mysqladmin tool, which is a client that lets you run administrative commands. For example, this command says to connect to MariaDB as root using the Unix socket and return the version:


        ```
        sudo mysqladmin version
        ```

        you will receive output similiar to this

        ```
        Output
        mysqladmin  Ver 9.1 Distrib 10.3.22-MariaDB, for debian-linux-gnu on x86_64
        Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

        Server version		10.3.22-MariaDB-1ubuntu1
        Protocol version	10
        Connection		Localhost via UNIX socket
        UNIX socket		/var/run/mysqld/mysqld.sock
        Uptime:			4 min 49 sec

        Threads: 7  Questions: 467  Slow queries: 0  Opens: 177  Flush tables: 1  Open tables: 31  Queries per second avg: 1.615
        ```

    * Step 7

        if you configured a separated administrative user with password authentication , you could perform the same opration by typing 

        ```
        mysqladmin -u admin -p version
        ```

6.  MySQL (MariaDB) Not Starting [closed]

    * __ERROR__
        if you see error this warning

        ```
        Job for mariadb.service failed because the control process exited with error code.
        See "systemctl status mariadb.service" and "journalctl -xe" for details.
        ```

    * __Solving__
        ```
        cd /var/lib/mysql
        ls
        rm -r *
        mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
        ```

        then by adding correct package list and signature

        ```
        sudo apt-get install software-properties-common
        sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
        sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] http://mariadb.mirrors.ovh.net/MariaDB/repo/10.3/ubuntu bionic main'
        sudo apt update
        sudo apt install mariadb-server
        ```
        

7. Solving the “Too many levels of symbolic links” Error Or Forbidden( 403 ) when access file in /var/www

    * __solving__
        straight to solving :
            when symlink use to /var/www
            ```
            ln -s dir_source /var/www
            ```
        it not open or access this dir_source in /var/www because permittion

        You Can fix this issue with change mode to user or root permition
        ```
        sudo chmod 755 -R /var/www/dir_source
        ```
        and then change owner to www-data because should www-data permition in /var/www
        ```
        sudo chown www-data:www-data /var/www/dir_source
        ```

8. When create Virtual Host in Nginx ( Virtual Block ) not working 127.0.0.1:8081 in /etc/hosts
    <br/>
    * __error__
    Most web developers have adopted the practice to test locally using, for example, port 8080 or anoter port. One might wonder we can also accomplish this with /etc/hosts. For example, can we add the following line to the hosts file:
        ```
        127.0.0.1:8081       yourdomain.example.com
        ```
    unfortunatelly it can't ,The hosts file only deals with hostnames , not ports.

    <br/>

    * __Solving__
    To make work it , we can use a reverse proxy. A reverse proxy is typically a webserver like nginx.
    thats takes client requests and directs them to the appropriate backend server, These Backend servers can run on a different host and, more interesting to use a different port.

    Let’s take a look at how to configure this with Nginx. We can easily install nginx from our package manager like yum or apt-get. Its default installation folder is /etc/nginx.

    To configure a reverse proxy for baeldung.com, we add the following in a file called /etc/nginx/conf.d/baeldung.conf:
    ```
        server {
            listen 80;

            server_name baeldung.com;

            location / {
                proxy_pass http://127.0.0.1:8080/;
            }
        }
    ```
    When we use this config in /etc/hosts together with:

    127.0.0.1 yourdomain.example.com

    in /etc/hosts, nginx will receive our requests for yourdomain.example.com and direct those to the webserver running on 127.0.0.1:8080.


    9. When you want to swith php version in ubuntu

        * check your php version

            ```
                php -v
            ```

        * install php version you want.Example to version8.1
            ```
                $ sudo add-apt-repository -y ppa:ondrej/php
                $ sudo apt update
                $ sudo apt install php8.1
            ```

        * you can disabled old version php use
            ```
                sudo a2dismod your_old_php_version
            ```

        * you can enabled new version php use
            ```
                sudo a2enmod php5.6
            ```
        
        * Or you can swicth use:
            ```
                sudo update-alternatives --config php
            ```
    10. when you want to copy pub ssh key in ubuntu
        * make sure you has install and setting pbcopy & pb paste to make your job easier.

            a. install x-clip 
                ```
                    sudo apt-get install x-clip -y
                ```

            b. edit your BASH settings file using your favorite text editor, example using nano
                ```
                    nano ~/.bashrc
                ```
            c. then create an alias for pbcopy and pbpaste
                ```
                    alias pbcopy='xclip -selection clipboard'
                    alias pbpaste='xclip -selection clipboard -o'
                ```
        
        * and finally you can copy your ssh public file.
            ```
                cat ~/.ssh/id_rsa.pub | pbcopy
            ```

    11. if net::ERR_ABORTED 504 (Gateway Timeout) vite svelte

        ```
            node ./node_modules/esbuild/install.js
        ```