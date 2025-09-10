# Database Schema

![image](../../../Assets/4-1.png)

## Clue provided

1. Find out where this information could come from. Then craft an attack string against an endpoint that offers an unnecessary way to filter data.
2. Find out which database system is in use and where it would usually store its schema definitions.
3. Craft a UNION SELECT attack string to join the relevant data from any such identified system table into the original result.
4. You might have to tackle some query syntax issues step-by-step, basically hopping from one error to the next.
5. As with "Order the Christmas special offer of 2014" this cannot be achieved through the application frontend.

## Solution

### Identifying vulnerability

The vulnarability used in this challenge is SQL Injection. We can exploit this vulnerability to extract the database schema information. The vulnerable endpoint is the one used to search for products:

```
http://localhost:3000/#/search?q=
```

![image](../../../Assets/4-3.png)

### Exploiting the vulnerability

We can use union-based SQL injection to extract the database schema information. The database system in use is SQLite, which stores its schema definitions in the `sqlite_schema` table.

To extract the schema information, we can use the following payload using burpsuite:

```
'))+UNION+SELECT+1,+2,+3,+4,+5,+6,+7,+8,+sql+FROM+sqlite_schema--
```

### Result

![image](../../../Assets/4-4.png)
![image](../../../Assets/4-5.png)


## Additional Information

From this challenge, we learn the existence of item with id 10 which is the "Christmas Special Offer of 2014". This item will be used in the next challenge.

![image](../../../Assets/5-1.png)