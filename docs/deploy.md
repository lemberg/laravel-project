# Deploy

## Development Server

Deploy command

```
$ ansible-playbook -i config/deploy/hosts config/deploy/deploy-dev.yml
```


## Setup 

Install **Ansible** and **Ansistrano**

```
$ ansible --version
ansible 2.1.1.0
```

Install [Ansistrano playbooks](https://github.com/ansistrano/deploy#installation)

```
$ sudo ansible-galaxy install carlosbuenosvinos.ansistrano-deploy carlosbuenosvinos.ansistrano-rollback --ignore-errors
```



## Local ssh config and ForwardAgent

Add host-alias to ssh config.
 
```
$ cat ~/.ssh/config

# development server
Host development-server-ssh-alias
   Hostname localhost
   Port 22
   User FIX_USER_NAME
   ForwardAgent yes
# EOT development server
```

Then use only host-alias on the **inventor** **hosts** file



## First run

Steps for prepare deploy environment, just example paths.

1. Server must satisfy all requirements
2. Prepare folders and environment

    ```
    $ mkdir -p /tmp/deploy/shared
    $ cp -r ./storage /tmp/deploy/shared
    $ cp ./.env.example /tmp/deploy/shared/.env
    ```
3. Create temporary current folder and `artisan` file

    ```
    $ mkdir -p /tmp/deploy/current/public
    $ touch /tmp/deploy/current/artisan
    
    ```
5. Add **APP_ENV** and **APP_KEY**

    ```
    $ vim /tmp/deploy/shared/.env
    ``` 
    
    Example
    
    ```
    APP_ENV=production
    APP_KEY=base64:eBzXep0nTYQg4TBGgibKB98C0P9GHdBoolmsOzLNksg=
    ```
