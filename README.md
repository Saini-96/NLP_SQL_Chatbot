# NlpSQL


NlpSQL is a question answering system that uses natural language processing to generat SQL statements.
I used `NLTK <http://nltk.org/>` to parse the text and created a parse grammar to build the SQL query.
The goal of the project is to create an easy way for regular to fetch data from the database even if they don't know SQL language.
The database engin used in this project is `MySQL <https://www.mysql.com/>`


Markdown ![NLP-SQL Translation Architecture](/root/nlpSql/NLP-SQL.jpg)
Markdown ![Image](/root/nlpSql/NLP-SQL_2.jpg)

Requirements
------------
You will need some Python packages

I have already created a virtual enviroment by typing : source nlpSql/bin/activate then there will not be any need of package installation.

To install dependencies (on a Debian-like GNU/Linux distribution):
    cd NlpSQL
    	apt-get install python-tk python3-tk
		pip install nltk
		apt-get install python-dev libmysqlclient-dev
		pip install MySQL-python
		apt-get install mysql-client-core-5.7
		apt-get install mariadb-client-core-10.0
		apt-get install mysql-server
		apt-get update && sudo apt-get dist-upgrade

For starting SQL Server /etc/init.d/mysql start

You will also need to download some NLTK data package. You can do so executing:

    python -m nltk.downloader genesis maxent_treebank_pos_tagger punkt stopwords averaged_perceptron_tagger

You will also need MySQL database. You can do so & have it by running following command:

    apt-get install mysql

Now you would need to create the databse schema provided. 
A good tutorial [Create a MySQL Database on Linux via Command Line](https://www.liquidweb.com/kb/create-a-mysql-database-on-linux-via-command-line/)

Please make sure to name the database `employees`
Ok, Now we will need to papulate the data:

    mysql -u root -p
    mysql>
	  CREATE DATABASE employees;
	  SHOW DATABASES;
	  exit

    mysql -u root -p employees < schema.sql #for filling database with sql schema

You would need to update the config file to connect to the databse by filling the data:

    nano config.py

Then Change the following:

    db_config = {
        'user': 'root',
        'passwd': 'root@123',
        'host': '127.0.0.1',   
        'db': 'employees',
        }

That's it!

Runing
----------
Make sure you fulfill the requirements First.

To run:

    python main.py
----------



for troubleshooting in mysql (authentication related issues)

/etc/init.d/mysql stop
mysqld_safe --skip-grant-tables &
mysql -u root -p
>use mysql;
>update user set authorization_string=password("root@123") where User="root"
>flush privileges;
>exit
/etc/init.d/mysql start
