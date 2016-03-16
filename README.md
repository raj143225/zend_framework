#DB Design Guidelines for **Rapid Funnel**

Created By: Rajkumar and Neeraj  
Date: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;16th March 2016  
This document is applicable only for **Rapid Funnel** application.


**Storage Engine:**
- Choose storage engine smartly based on the data in tables.
[Storage Engines](https://dev.mysql.com/doc/refman/5.0/en/storage-engines.html)


**Tables:**
- Table names will be in lower case.
- In case of multiple words then follow **camelCaps** capitalization convention. 
e.g:  for "users payment info" name should be **usersPaymentInfo**

**Fields:**
- Field names will be in lower case. 
- In case of multiple words then follow **camelCaps** capitalization convention. 
e.g for "user id" name should be **userId**

**Foreign Keys:**
- If  a table has a foreign key column of another table then the column will be like
**userId**
where user is the singular of users **(table name)** and **id** is the reference column name in users table.

**Collation:**  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**utf8_general_ci** for all char, varchar or text fields.

**Datatypes:**
- Should be choosen smartly.
- Choose datatype as timestamp instead of datetime (if allowed) as datetime takes 4 bytes where as timestamp is only 2 bytes.
- Using tiny int instead of enum (in fileds like status or user types) as tiny int takes only one byte where as enum one or two bytes based on the options (Please do not forget to add proper comment)
-  Look into datatypes properly before choosing for the field like **TINYINT, SMALLINT, MEDIUMINT** and **INT** which take 1, 2, 3 and 4 bytes respectively.

**Field Size:**
- Choose appopriate Field Size for columns.  
Like a name should not be VARCHAR(255), as in real a name won't be 255 characters long.

**Points to Takecare:**
- Avoid allowing Null in fields if possible.
- Use unsigned instead of signed if the column is expected to take only positive values like auto increament fields.
- Use comments wherever required.
