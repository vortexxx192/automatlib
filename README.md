#automatlib

####Python library to solve the dynamic matching problem efficiently. It was written during the university research, so don't treat it as something useful in production (but you are welcome if you want).

Assume we have a set of words *S* and we want two perform two operations:
- **add(w)** -- add word *w* in *S*
- **search(T)** -- find all words from *S* that are present in text *T* as substrings.

####Usage instructions in Russian:
Я переписал всё на Python, потому что он проще и понятнее. А еще потому что написанный на С++ код очень плохой и его все равно пришлось бы переписывать с нуля.

###Необходимые программы
- **Python 2.7.8** -- скачивать с https://www.python.org/downloads/
- Менеджер пакетов **pip** -- инструкции по установке здесь: https://pip.pypa.io/en/latest/installing.html
- Пакет **graphviz**. Устанавливается выполнением команды ```pip install graphviz```
- Опционально -- **git**. Можно и без него, но лучше с ним. Иначе, что ж мы за программисты такие, без git'а.

###Как что-нибудь сделать
1. Склонировать репозиторий с https://github.com/vortexxx192/automatlib. Делается это командой ```git clone https://github.com/vortexxx192/automatlib.git```. Ну или нажатием на гитхабе кнопочки **Download ZIP**.
2. Перейти в нужную директорию: ```cd automatlib/automatlib```. 
3. Запустить интерпретатор командой ```python```.

####Обычный Ахо-Корасик
Давайте теперь, к примеру, построим один автомат на словах *'his', 'she', 'hers'* и в каком-нибудь тексте их поищем.

```py
>>> from AhoCorasick import AhoCorasickAutomaton as AC # импорт нужного класса
>>> aut = AC(["his", "she", "hers"])  # строим автомат по списку слов
>>> print(aut.search("aaahishe"))  # пропустим через автомат строку
```
Вывод должен быть ```['his', 'she']``` -- именно эти слова присутствую в тексте в качестве подстрок.

Можем нарисовать автомат. Но, из-за большого количества ребер, он получается не очень. Мне так и не удалось научиться нормально отрисовывать автоматы. Но, тем не менее, сделать это можно так:
```py
>>> aut.toGraphvizSource()
```
Не стоит пугаться вывода -- это код graphviz. Загляните в текущую директорию -- там есть файлик *automaton.png*.

####С добавлениями
Теперь сделаем то, ради чего все затевали.
```py
>>> from DynamicAC import DynamicAC   # импорт нужного класса
>>> aut = DynamicAC()     # создание объекта
>>> aut.add('his')    # добавим слово в множество
>>> aut.add('her')    # добавим еще одно
>>> aut.add('banana') # ну и третье
>>> aut.search('hisbananainbandana')  # ищем вышедобавленные слова в тексте
```
Вывод будет ```['his', 'banana']```.

###Заключение
Have fun.
