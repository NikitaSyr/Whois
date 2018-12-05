h1 Результаты работы 

Выводит список доменов, начинающихся с https

```python
import re 

o = open('result.txt', 'w') 
g = 0
with open("too.txt") as file: 
    for line in file: 
        
        urls = re.findall('https:[\/0-9a-zа-я\.\-_]+', line) 
        if urls:
            g = g + 1
            print(urls) 
print(g)
o.close()
```  

Модифицируя этот код можно настроить его для работы с whois

Код указан в отдельном md файле для удобства: https://github.com/NikitaSyr/Whois/blob/master/code.md

В результате, код выдаёт ошибку, так как все библиотеки whois для python 3 просто не работают

```python
AttributeError                            Traceback (most recent call last)
<ipython-input-4-8b5673b1efb3> in <module>()
    117             domains = urls
    118             for dom in domains:
--> 119                 d = whois.whois(dom)
    120                 print(d.avaliable)

AttributeError: 'dict' object has no attribute 'whois'
```  

