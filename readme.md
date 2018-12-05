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

Поэтому воспользуемся ручным вводом. Для этого нам понадобиться более удобный список доменов начинающихся на https:

```python
import re
import whois
from urllib.parse import urlparse

filename= open("too.txt","r")
fileout = open('result.txt', 'w')
pattern = re.compile('https:[\/0-9a-zа-я\.\-_]+')
domain_list=list()

for line in filename:
    domain_list.extend(pattern.findall(line))
d = 0
for item in domain_list:
    d = d + 1
    domain=urlparse(item)
    fileout.write(domain.netloc+'\n')
    print(domain.netloc)
    
fileout.close()

```  

