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
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/850a8d55-d8eb-419c-838b-0814d724b1a1)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/704c742c-ccf7-4303-846e-b6c3b6526d8f)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/5f7bea7b-845a-485f-8f53-b110ca38cdcd)
Click on the menu Login/Register and register for an account 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/810a3311-b71a-4832-920f-6ce1d2300e17)
Click on the link “Please register here”
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/b4b277ec-a4fd-4d2d-88a0-53d4de2980eb)
Click on “Create Account” to display the following page:
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/20312b73-35bd-4e94-82ec-b6ab47ec7fcb)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page. 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/94a3f1d1-f683-45dc-8247-197743109158)
Click “Login”. The logged in page will show as below:
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/27a9585a-63d6-4a90-bb50-f040a262592b)
login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password. 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/b38d644b-287b-4972-81a4-0ea86647f5b2)
Click the login button and you will see it enter into the administrator page.
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/8fbe7398-b224-4938-9c17-60565908de7b)
# Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below: 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/f2329720-887c-48f7-be98-f5a6479b6f22)
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/db6e5ac7-9aab-49d9-93b5-65039fe10212)
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/9737f980-188f-4525-9648-b16f9335be84)
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/9eaa6a6e-ff20-418b-9d2f-fecdddcb2b7c)
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/28c0f8e8-0ec0-4425-93fa-94781387e446)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned. 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/8442469e-362d-48a4-915c-d0aebe490064)
ince we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/8c76c295-b529-4dfb-99db-7e9248d6884d)
After adding the order by 6 into the existing url , the following error statement will be obtained: 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/9c0f38a1-ff94-4959-bc46-490135231865)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/5165e616-74e9-4847-b214-bd14bf5ea38c)
As it is having 5 columns the query worked fine and it provides the correct result.
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/ba6bfd81-ce12-4bb3-b921-72a478ab19d1)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5) 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/c64d8e45-73c6-43df-a6df-f3323af48303)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/031507bd-6870-480a-b58e-9e03968162a3)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/330fc46d-5a6f-437c-ad7d-8a086ae71211)
 The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/8f114f64-f518-4c51-9305-b441bbf19733)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords
When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/729f4718-1446-458f-bcf6-e8652e76af69)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/b353dab2-5379-452d-83df-34efe160691f)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/09b8b9e8-679f-46cd-94be-adc8b53bd5a5)


Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details 
![image](https://github.com/sachinezhilmaran/sqlinjection/assets/128135351/ad76ef59-c211-4a3d-b68a-c589586cce08)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
