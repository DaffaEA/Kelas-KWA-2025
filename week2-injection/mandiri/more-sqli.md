# More sqli

![image](../../Assets/9-1.png)

## Identifying the vulnerability

We are welcomed by login form

![image](../../Assets/9-2.png)

if we test an invalid credential, we will get an error message

![image](../../Assets/9-3.png)

## Exploiting the vulnerability

we can use this to do sql injection

```
username : whatever
password : ' or '1'='1
```

at first we get no flag, but if we try to login with burpsuite by intercepting the request and use repeater, we get the flag

![image](../../Assets/9-4.png)


