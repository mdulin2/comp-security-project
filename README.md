# comp-security-project

For the first week of the project, Trevor spent time using Google to 
understand what an SQL injection is, and how to perform one.  An SQL
injection is a web-based attack wherein the attacker might gain access
to a system by using SQL syntax in a form text entry field.  

In a Login form, the backend program might utilize code that takes the
user's entry and stores it in a variable called userIDEntry.  Then, the
JavaScript code would look like this code from 
https://www.w3schools.com/sql/sql_injection.asp:

``` JavaScript
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = " + txtUserId;
```

To view information about the system, the attacker might provide the
entry:

```
105 OR 1 = 1
```

The resultant SQL entry would then be

```
SELECT * FROM Users WHERE UserId = 105 OR 1 = 1;
```

This would return the Users table for the attacker to see.  If the
Users table also contains passwords, then the attacker has attained
a complete list of usernames and passwords for the site.  Similar code
can also be used to gain unauthorized access to a system.