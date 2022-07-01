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
       







    








