---
layout: post
title:  "Journal #Nine [DAT602] - Password Security" 
author: Dale Stephenson
categories: [ DAT602, Journal, Password Security ]
image: assets/images/DAT602-J9.jpeg
featured: true
hidden: true
---
<i>Password Security</i>

JOURNAL #NINE [DAT602]

<h2>Password Security</h2>

As part of the DAT602 milestones, development work has progressed on the procedure that will be used to create the real gameplay. As part of this development work research has been conducted into securing the database, in particular the safe securing of password credentials.
 
<h3>WHAT</h3>
 
The database stores player passwords in the player table. During the first milestone, no consideration was made to the safe securing of passwords and as a result, they were stored in plain text, which is a severe mistake in any database as this makes them incredibly vulnerable.
 
One of the procedures that make up the milestone brief for the database is the ability for a new player, or user, to register an account. The account information for each user must be safe to mitigate the risk of an attack vector, it is important therefore that the password input is encrypted.
 
The password encryption chosen is the AES (Advanced Encryption Standard) algorithm, also known as 'Rijndael', AES encodes with a 128-bit key.
 
<h3>WHY</h3>
 
AES encryption was chosen as it offers the best defence in terms of security and is often considered to be the gold standard, which is why it's certified by NIST and used by the US government to protect data. Other algorithms such as MD5 and SHA1 do not offer the same level of protection because exploits for both of these are common. Despite this, either of these are better options than storing passwords in plain text.
 
To offer further protection for database users, particularly those that use weak passwords, the storing of passwords will deploy salt. Salt is a term used in cryptography that describes a hash that is generated by combining the password input with a randomly generated text string.
 
For the game database, the salt stored will be unique for each user of the database. Using unique salts for each user not only helps to keep them safe from attack vectors such as rainbow attacks by protecting passwords that are dictionary words, but it also prevents two different users from having the same hash where they have used the same password.
 
<h3>HOW</h3>
 
Before accepting passwords that could be passed as AES encryption the table needed to be updated, the password column data type was changed to BLOB from varchar. Once this was done the procedure was updated to set the password input as AES_ENCRYPT and a key string was passed alongside the password.
 
Once the encryption was functioning correctly salt was added to the password, for these to be unique values against each user a new salt is declared for each procedure called using the UUID function. The new salt UUID is then included as part of the password. The salt in the database is set as varchar(36) and placed at the beginning of the password as input by the user. 

Encrypting passwords stored in a database, combined with unique salts, mitigates the risk that the passwords are cracked, UUID is a useful tool due to its randomness and uniqueness. The same password encryption used when registering a new user is also used when that user logs into their account.

The following screenshot shows the working password input used in the registration process in the game:

<center><img src="/assets/images/DAT602_PasswordSecurity.png" alt="Password Security"></center><br>

<i>References</i>

Bichot, G. (2015, October 14). Storing UUID Values in MySQL Tables. MySQL Server Blog. [https://mysqlserverteam.com/storing-uuid-values-in-mysql-tables/](https://mysqlserverteam.com/storing-uuid-values-in-mysql-tables/)

Frank. (2006, August 21). MySQL Consulting and NoSQL Consulting: MySQL DBA: Storing Passwords in MySQL. MySQL Consulting and NoSQL Consulting. [http://mysqldatabaseadministration.blogspot.com/2006/08/storing-passwords-in-mysql.html](http://mysqldatabaseadministration.blogspot.com/2006/08/storing-passwords-in-mysql.html)

How do you securely store a user’s password and salt in MySQL? (n.d.). Stack Overflow. Retrieved April 24, 2021, from [https://stackoverflow.com/questions/7270526/how-do-you-securely-store-a-users-password-and-salt-in-mysql](https://stackoverflow.com/questions/7270526/how-do-you-securely-store-a-users-password-and-salt-in-mysql)

MySQL - AES_DECRYPT ( ) Function. (2019, November 6). GeeksforGeeks. [https://www.geeksforgeeks.org/mysql-aes_decrypt-function/](https://www.geeksforgeeks.org/mysql-aes_decrypt-function/)

MySQL :: MySQL 8.0 Reference Manual: 12.24 Miscellaneous Functions. (n.d.). Retrieved April 24, 2021, from [https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid)

Salted, M. G. U., Hashed, February 09, L. was published on, & 2015. (n.d.). MySQL: Generate Unique Salted, Hashed, Logins. Boone Putney. Retrieved April 24, 2021, from /development/mysql-generate-salted-hashed-logins/

Salting and hashing passwords in MySQL. (n.d.). Stack Overflow. Retrieved April 24, 2021, from [https://stackoverflow.com/questions/23278565/salting-and-hashing-passwords-in-mysql](https://stackoverflow.com/questions/23278565/salting-and-hashing-passwords-in-mysql)

Storing passwords in a secure way in a SQL Server database. (n.d.). Retrieved April 24, 2021, from [https://www.mssqltips.com/sqlservertip/4037/storing-passwords-in-a-secure-way-in-a-sql-server-database/](https://www.mssqltips.com/sqlservertip/4037/storing-passwords-in-a-secure-way-in-a-sql-server-database/)

Storing passwords securely with MySQL encryption. (n.d.). Zino UI. Retrieved April 24, 2021, from [https://zinoui.com/blog/storing-passwords-securely](https://zinoui.com/blog/storing-passwords-securely)
