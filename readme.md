Результаты домашней контрольноц работы 
=====================

Код программы, написанной на python3. Он выводит список доменов, начинающихся с https

```python
import re 

o = open('result.txt', 'w') 
with open("too.txt") as file: 
    for line in file: 
        
        urls = re.findall('https:[\/0-9a-zа-я\.\-_]+', line) 
        if urls:
            print(urls) 
print(g)
o.close()
```  

Код выдаёт подходящие домены в таком формате:

![](https://pp.userapi.com/c845522/v845522489/14c36d/CzgJQHvJo1g.jpg)

Модифицируя этот код можно настроить его для работы с whois

[Код указан в отдельном md файле для удобства](https://github.com/NikitaSyr/Whois/blob/master/code.md)

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

Поэтому воспользуемся ручным вводом. Для этого нам понадобиться более удобный список доменов начинающихся на https. Для этого создадим простой цикл, который будет выдавать нужные домены из списка. На сайте REG.ru есть возможность проверять единовременоо до 500 доменов на занятость. Будем вручную выбирать по 500 доменов из ~9300

Пример кода для вывода списка из доменов с 500 до 1000-го (пришлось изменить способ поиска для вывода доменов без лишних кавычек и чёрточек)

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
    if (d > 500) and (d < 1000): 
        domain=urlparse(item)
        fileout.write(domain.netloc+'\n')
        print(domain.netloc)
    
fileout.close()

```  

Проделав это и пытаясь вставить 500 доменов на сайт REG.ru он выдаёт ошибку, что нельзя делать столько запросов. Методом тыка я выяснил, что сайт REG.ru позволяет работать с 50 доменами. Так же часто выходит уведомление, о том что превышен лимит запросов к whois и мой ip банится на небольшой промежуток времени. 

Так же я перебрал варианты пакетов для python3 , я попробал сделать это задание с помощью whois, python-whois и urlopen

С помощью сервиса[seocafe](http://info.seocafe.info/tools/massdomcheck/) мне удалось запустить долгую проверку всех 9338 доменов. Так же этот сервис отбросил дубликаты доменов, сократив общее число для поиска до 3984. Почти сразу мне удалось увидеть свободный для регистрации домен!

![](https://pp.userapi.com/c845520/v845520006/14c36c/qkKgwUHQP9s.jpg)

Ещё сайт, доступный для регистрации:

![](https://pp.userapi.com/c845520/v845520006/14c37e/gQ3DayPpZNM.jpg)

Процесс работы:

![](https://pp.userapi.com/c845520/v845520006/14c3a5/kCydC5CU4kY.jpg)

Так же, в процессе поиска информации сервис выдавал, что домен доступен, однако после проверки на REG.ru выдавало, что домен занят.

Выгрузки использованного реестра:

[домены, сохранённые первым способом](https://github.com/NikitaSyr/Whois/blob/master/Result1.txt)

[домены, сохранённые вторым способом](https://github.com/NikitaSyr/Whois/blob/master/result.txt)
