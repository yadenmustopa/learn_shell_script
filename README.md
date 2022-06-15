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

        



    








