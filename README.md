# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/4db742df-f86e-42b5-8b43-164bd8e92d4d)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/7fa52bbe-7357-470b-a2a2-f7f366f1f0c7)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/d64bd86e-7869-4440-8ecd-90d6fc6b1ff5)

Click on the link “Please register here :

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/37e2e09f-058e-45de-b217-bc6729b81a25)

Click on “Create Account” to display the following page

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/f911dad4-31b7-484a-93d9-25761bf5b278)

Click “Login”. The logged in page will show as below

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/12c287e6-5c1d-4701-bc63-2da3a869679e)

### Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/dc56fc0b-064e-4b91-98f9-00f6024efa9b)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/df4412e4-ba4b-4021-81d4-d1ad2b4c8220)
### Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/30f56152-baed-41f2-8c99-95606cc90c06)

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/475c4c14-13b3-41b4-9d05-38e2742cdb89)

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/fe47322c-934f-4424-a479-868c394cc13e)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/ca1d8208-d631-4c56-bbd3-340160a98a0e)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
The browser url of this info page need to be modified with the url as below:
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/c580f41d-af7a-4844-a8e5-3230f6a6d199)
After adding the order by 6 into the existing url , the following error statement will be obtained
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/f13a6cf4-af52-4bfc-93b1-244dee8162f8)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/88d47d77-42c8-4958-8258-fcbc88526d72)
As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/d2852de5-1f5c-40ac-a97b-9c722e75217b)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/cbe9925d-7ab3-41fe-8fd0-dec2256b5c07)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/bf4d6443-e64c-4a68-ab96-f76309b514ce)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/29e298c8-9e46-4c01-8c69-6c5fdd2d428b)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.
Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/cc89837e-0303-43d3-b3ba-471479307269)

The url once executed will retrieve table names from the “owasp 10” database. ### Extracting sensitive data such as passwords
When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/3118daa1-36db-49a2-9420-fad68c093e73)

The column names of the accounts is displayed below for the following url:
http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/17f2c1e3-4515-4c89-baf1-49862ee2e496)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.
Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/116696f7-20ea-4bd5-9f42-daab4cb1e93f)

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/ac04a65a-b7ff-4d3e-8f82-3cebf5869355)

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/b0036b0c-7821-4930-a6ce-87a1350a0151)

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/923d2597-1bc1-4fad-a4b9-929be765dfd9)

![image](https://github.com/Dhanashreemullaithasan/sqlinjection/assets/94165415/491848e4-d00c-47be-a863-cdfac8dc53f8)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

RESULT:
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
