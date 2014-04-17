---
title: Databases and Migrations and Sequel, Oh my!
date: 2014-04-15 04:32 UTC
tags:
---


##### Now if only I had Courage, a Heart, and a Brain ;)

It was inevitable. The task of capturing data and incorporating databases to our applications has become a reality. Remember that URL Shortener site I talked about? Well, we added another layer to the complexity. And quite frankly, as overwhelming as it sounded at first; databases, postgres, and migration is just like any other topic we’ve learned here at gSchool. Big, bad and daunting at first, then manageable and dare I say, even “fun” to play around with.

Put simply, a database lets us store relative information in a table format. This makes it especially easy to retrieve information and therefor, sequently manage that information.

We all know that you can create a database within postgres in your command line. But  when you have larger apps that need testing that can become a bit of a lengthy task. The [sequel gem](https://github.com/jeremyevans/sequel) helps you incorporate those same commands that you would run in your terminal, within your app. From there, you create a scripts directory and a file within that titled create_database.sql. The contents of that file are the same as the postgres commands and should look like this:

CREATE DATABASE (preferred database name)development;


CREATE DATABASE (preferred database name)test;

Now, in order for those databases to be truly created within your local environment, you run in your command line:

![Database Creation](/images/create_database.png)

Voila! Your databases are there and ready to populate with all kinds of information that your app will collect. To create a table within the databases you will create a migration. Migrations are ruby files within your app that contain commands that make incremental changes to a database’s schema and data. You can have hundreds of migrations executing commands to create new tables, add columns, rename tables and columns, alter tables, add indexes etc. Migrations should be in their own directory in your app. Your first migration’s file name starts with the migration number and then essentially what that migration is implementing. Such as, 001_create_table.rb.

In that file you want the commands to make said table. Below, you’ll see a typical example of what migration looks like:

![Migration](/images/migration.png)

Just like like the database you need to run this string in your terminal to apply the changes to both your databases.
Keep in mind the general setup of your migration command should look like this
 $ sequel -m (directory name) postgres://(username):(password)@localhost(port)/(database)

Development Database:
![Migration command](/images/migration_command.png)
Test Database:
![Migration command](/images/migration_test.png)

Now, both of your databases are up to date with the latest changes.

For small apps your test database string will be defined in your spec_helper. There will be an almost identical line in your config.ru with the exception that this one will be the path to your development database rather than the test.

![Database connection string](/images/db_connection.png)

When dealing with larger applications that hold more than 2 databases, such as a Heroku staging and production, things can get a little more tricky. There are different commands to run those databases and migrations separate from your local ones. The database strings will most likely be in your .env file to ensure your password is protected. More than likely you will have a line like this that defaults to the right database when that database is called throughout your application.

![Database connection string2](/images/db_connection2.png)

So, there you have it. Database Incorporation.
