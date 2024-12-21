---
title: "HTB Sherlocks:Bumblebee Writeup"
date: 2024-01-10T09:09:47+05:30
draft: false
params:
  slug: "sherlocks-bumblebee"
layout: "post"
tags: ["Sherlocks", "HTB"]
authors: ["Lordsudo"]
---
![banner](https://gist.github.com/user-attachments/assets/9a9b528d-89c0-47ba-af23-7715f0369989)

# HTB SHERLOCKS - BUMBLEBEE
-----

## Description

An external contractor has accessed the internal forum here at Forela via the Guest WiFi and they appear to have stolen credentials for the administrative user! We have attached some logs from the forum and a full database dump in sqlite3 format to help you in your investigation.

## Files Attached
![Files](https://gist.github.com/user-attachments/assets/6fbcf707-1bf3-407f-a425-ab6bf23db7de)

-----
## Solution

We shall use a DB Browser for SQLite to make analysis easier. This can be downloaded from https://sqlitebrowser.org/.

Loading the database file we can see that we have various tables and can now begin analysis.

![sqlite db](https://gist.github.com/user-attachments/assets/65761d69-82a5-4054-9244-0ee2bd10dfee)

-----
### Task 1 - What was the username of the external contractor?

Checking through the various tables, we find one called ```phpbb_users``` and come across usernames that have an email with a domain ```@contractor.net```. This gives us the username of the external contractor.

*Flag: apoole1*

![username](https://gist.github.com/user-attachments/assets/17289781-546d-44fc-b426-c1f65a39bcd7)

-----
### Task 2 - What IP address did the contractor use to create their account?

Checking through the same table, we can find the IP address in a column called ```user_ip``` and cross referencing with the username we get our IP address.

*Flag: 10.10.0.78*

![ipaddr](https://gist.github.com/user-attachments/assets/d282f3a8-dda7-4932-83d4-09611af06a78)

-----
### Task 3 - What is the post_id of the malicious post that the contractor made?

Sifting through the tables, we can see one that is named ```phpbb_posts``` and since we know the attackers IP address, matching that we can get the post_id  of the malicious post made from the column ```post_id```

*Flag: 9*

Skimming through the ```post_text``` we could speculate that the malicious actor probably tried to set and check for cookies specifically ```phpbb_token``` in this case which confirms that it is indeed malicious.

![postid](https://gist.github.com/user-attachments/assets/1c0aa979-ef18-4e1d-850b-3a9e0f11ef86)


-----
### Task 4 - What is the full URL that the credential stealer sends its data to?

We could analyse the malicious text found in the column ```post_text``` and filter by the attacker's IP address. 
This gives us the full URL we were looking for.

We filter by his IP address, since we think that he was trying to steal cookies and hence would want them to be reflected back to him.

*Flag: http://10.10.0.78/update.php*

![urlpath](https://gist.github.com/user-attachments/assets/a47b6d89-6a0e-4c98-9bd7-6d68f4e9e8f4)

-----
### Task 5 - When did the contractor log into the forum as the administrator? (UTC)

We can analyse the ```phpbb_log``` table and see if we can get records for a succesful login attempt.
Bingo! We can see a record for ```LOG_ADMIN_AUTH_SUCESS``` under the ```log_operation table``` and the IP address confirms it is indeed the contractor.


![logintime](https://gist.github.com/user-attachments/assets/3a013ab6-353e-433b-b94d-b059b6838750)

We can then pick the record from the ```log_operation``` table and use an online converter to change it to human-readable format and this gives us the time in UTC.
The converter used is https://www.epochconverter.com/

*Flag: 26/04/2023 10:53:12*


![Timestamp](https://gist.github.com/user-attachments/assets/4f9086eb-9e9f-4ae6-9462-5817d677347f)
-----
### Task 6 - In the forum there are plaintext credentials for the LDAP connection, what is the password?

We can check through the ```phpbb_config``` table and search for ```ldap``` which gives us the password.

*Flag: Passw0rd1*

![ldappd](https://gist.github.com/user-attachments/assets/118a0578-ec68-4f4c-953e-245c24d29b2f)
-----
### Task 7 - What is the user agent of the Administrator user?

We know the IP address of Forela ```10.255.254.2``` and can filter by it in the ```access.log``` to get the user agent.

*Flag: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36*


![useragent](https://gist.github.com/user-attachments/assets/0074e984-ec8e-4681-83d3-f307a987f168)
-----
### Task 8 - What time did the contractor add themselves to the Administrator group? (UTC)

Tracing back to the point where we identified the succesful login, we can also see a record for ```LOG_USER_ADDED``` and the ```log_data``` column entry shows us the user ```apoole``` is part of the ```Administrator``` group.

![adminadd](https://gist.github.com/user-attachments/assets/6d542e5c-f7a0-4b5d-a462-df9fec9cff16)

We can convert the timestamp to human-readable format and get the answer.

*Flag: 26/04/2023 10:53:51*


![timestampadmin](https://gist.github.com/user-attachments/assets/418a777b-1ade-41ae-84a9-59c984b9e0ec)
-----
### Task 9 - What time did the contractor download the database backup? (UTC)

While still in the ```phpbb_log``` table, we can see a record for a DB Backup and thus we can now search through the ```access.log``` for the time when he downloaded the backup.

Since we know it is a SQL Database, we could probably search for ```sql``` and we get the particular entry.
The entry also shows that it is a GET request and therefore we can confirm the attacker was trying to download the backup.


![sqlbackup](https://gist.github.com/user-attachments/assets/b7edd48a-a871-46ad-8f6f-84488544f2af)

From here, we can see the timezone is ```+0100``` and to get UTC we subtract one hour giving us the answer.

*Flag: 26/04/2023 11:01:38*

-----
### Task 10 - What was the size in bytes of the database backup as stated by access.log?

While analysing the entry for the backup download, we can find the file size indicated right beside the status code [200].

*Flag: 34707*

![sqlbackupsize](https://gist.github.com/user-attachments/assets/fdbe8fdf-bd67-4c78-a885-02d049cbb20b)

-----

Nos vemos en mi próximo artículo...


# ![favicon](https://gist.github.com/user-attachments/assets/62b93db8-5f62-45de-8ba1-c55dcf201000)
