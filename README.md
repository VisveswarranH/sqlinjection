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

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
![image](https://github.com/user-attachments/assets/c4a14835-d8d6-43b6-93b3-ee02e5e3d95d)


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.


![image](https://github.com/user-attachments/assets/e0c919b7-f936-4b58-8dbc-2ee2144069cc)


Select Multidae from the menu listed as shown above. You will get the page ;

Click on the menu Login/Register and register for an account

![Alt text](image-1.png)

Click on the link “Please register here”
![image](https://github.com/user-attachments/assets/5c743031-6d21-4caa-af7d-05e04277c0fb)

Click on “Create Account” to display the following page:
![image](https://github.com/user-attachments/assets/2c926cfe-b89d-40b7-be5c-ad0ca5d84a88)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “haritha” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/user-attachments/assets/da10e310-e026-4486-9132-3428bd0976b4)


Click “Login”. The logged in page will show as below:
## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
![image](https://github.com/user-attachments/assets/d0c97932-5458-469f-9602-e0c231b5f973)

![image](https://github.com/user-attachments/assets/f4739ae0-9843-48b6-bf60-c5fe28f8cec8)

![image](https://github.com/user-attachments/assets/e468a686-9a07-4448-a797-feb49c7e0393)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

![image](https://github.com/user-attachments/assets/a2c4f316-d8fd-47b9-9d10-e6e1ae0684e5)


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/user-attachments/assets/aafd515b-b50f-458b-b11b-0d2719907ee3)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![image](https://github.com/user-attachments/assets/c2690c33-9bb3-4124-9289-3daabb182108)

The column names of the accounts is displayed below for the following url:

![image](https://github.com/user-attachments/assets/a36af408-5477-4625-9435-527a8a08119f)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

![image](https://github.com/user-attachments/assets/7a143e54-211c-4100-b32b-545695e48d3b)
## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).
![image](https://github.com/user-attachments/assets/bacf81fb-785a-4d4f-91fb-d5e0ddf237d4)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

![image](https://github.com/user-attachments/assets/dfa6d873-645d-49d4-9078-bea29cf34dcf)
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
