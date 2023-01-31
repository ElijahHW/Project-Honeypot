# 🍯**The Honeybee Project**🍯

## **Overview**

This project belongs to Web Security Class. This document contains all information about the project for installing, managing and attacking our Honeypot.

Project Assignement can be found here: ["HoneypotProject.md"](https://leho-howest.instructure.com/courses/14316/files/1806231/download?download_frd=1)

## **Getting Started**

### **Website Notes**

* You can access the website whilst connected to the FortiClient-VPN at; ["rgp06.hp.ti.howest.be"](https://rgp06.hp.ti.howest.be)
* Running on HTTPS only.
* User - password for an administrator account (user : admin |password: adminiscool).

### **Server Notes**

* Server is running on; ex. Debian GNU/Linux 11.
* Recommend connecting with ["Windows Terminal"](https://aka.ms/terminal).
* Also running on HTTPS only.



### **Connect to Server**
SSH into our server with the following details;
* hostname; rgp06.hp.ti.howest.be
* username; killerb
* password; sexydorian

```yml 
 ssh killerb@rgp06.hp.ti.howest.be
```


## **Challanges**

* **Challenge one! Identify the vulnerable input (SQL Injection)**  
Try to inject SQL Code through the website to display the secret table stored in our Database.

```yml
First you have to find the broken input which is located on the indexStat.php page. 

By testing the input, we can see that he is vulnerable. 
Then, we can retreive table information and stuff with : 
    test' UNION SELECT table_name, "u", "u" from information_schema.tables-- -
When the secret table is identified and that we know the structure, we can display the secret.
    test' UNION SELECT secret, "u", "u" from really_secret_table-- -
```

* **Challange Two! - Insert yourself in the team database**  
Having solved the first challenge, use SQL Injection to insert your user into the team table in Databse.
```yml
Same input on the indexStat.php but we have to do an insert into the collector_team table. 

    '; INSERT INTO collector_team (id_team, name, title) VALUES (3, "Dog","Test");-- 
```

* **Challange Three! - Find XSS vulerable query**  
A input is XSS vulnerable, find it !
```yml
The searchbar on the index page is vulnerable to XSS. Try to search: 
    <script>alert('xss')</script>
```

* **Challange Four! - Break the website with a JS Alert**  
If you found the XSS vulnerable input, enjoy with it ! 
```yml
Now that we found it, we can try to retreive information with that exploit. Enjoy ! 
```

## **Kibana**
* url; http://192.168.10.26:5601/
* username; elastic
* password; bCfymLdJhiNlGLDUkHjB


## **Ansible**

The following ansible-playbook will;

* Install and configure: 
    * GIT | APACHE | PHP | MYSQL | PYTHON3 | PIP | PYOPENSSL | CRUPTOGRAPHY.
* Clones and configures Website
* Generates and applies SSL keys
* Enables and disables modifications
* Triggers angry bees. 

### **Clone the project**
```yml
git clone git@git.ti.howest.be:TI/2021-2022/s3/web-security/projects/project-06/honeybee.git
```

### **Run the playbook**
```yml
sudo ansible-plabook -i hosts HoneyTastesGood.yml
```
### **Ansible File Hierarchy**
```yml
Ansible

├── files
│   ├── honeybeeHTTP.conf.j2
│   └── honeybeeHTTPS.conf.j2
├── tasks
│   ├── config.conf
│   └── install.conf
├── vars
│   └── default.yml
│            
└── HoneyTastesGood.yml

3 directories,  6 files   
```

## **Authors** 

Contributors names ~

ex. elias.harvik-wright@student.howest.be  
ex. dorian.cerfortain@student.howest.be
 
