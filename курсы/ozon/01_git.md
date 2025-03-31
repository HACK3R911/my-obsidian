что такое git
как применяется
как хранит данные

Система контроля версий

Проблематика
Все начинается, когда вы просто хотите хранить историю изменений вашей работы

mymodule.py 1 
```python
# Previously I had some complex logic in this
# module, but I had to delete it due to reasons.
# Very sad!
def my_function(first, second):
	return first + second
	
def another_function(first):
	return first + 1
```

Вопросы: 
- Какие изменения были в данном файле?
- Когда они были? 
- Кто их вносил? 
- Почему их вносили? Какая была цель?
Без истории изменений – мы не знаем!

git = распределенная система для хранения коллективной истории изменений всех файлов в проекте.

Но как мы будем хранить изменения?
Варианты :
- Хранить все файлы всегда, целиком и полностью (лишняя инфа)

- Хранить только первую версию и наборы изменений, чтобы можно было воссоздать по ним содержимое файла на любой момент времени

И что такое "момент времени"?
Варианты: 
- Мы будем сохранять вообще все: каждую секунду, любое изменение (много копий) 

- Мы будем сами создавать законченные "версии" наших файлов, когда посчитаем нужным

А что значит "распределенная"?
"Распределенная" = можно хранить историю сразу в нескольких местах

Наборы изменений
Было 
```python
def my_function(first, second):
	return first * second + 10
```

Внесем первое изменение 
```python
def my_function(first, second): 
	return first * second + 10 
	
+++ def another_function(first): 
+++ return first + 1
```

Получим 
```python
def my_function(first, second): 
	return first * second + 10 

def another_function(first): 
	return first + 1
```

Внесем второе изменение
```python
+++# Previously I had some complex logic in this 
+++# module, but I had to delete it due to reasons. 
+++# Very sad! 

def my_function(first, second): 
	--- return first * second + 10 7 
	+++ return first + second
```

Получим
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return first + second
	
def another_function(first): 
	return first + 1
```

Итого
```python
def my_function(first, second):
	return first * second + 10
```
==**+**==
```python
+++ def another_function(first): 
+++ return first + 1
```
==**+**==
```python
+++# Previously I had some complex logic in this 
+++# module, but I had to delete it due to reasons. 
+++# Very sad!

def my_function(first, second):
--- return first * second + 10 
+++ return first + second
```
==**=**==
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return first + second
	
def another_function(first): 
	return first + 1
```

Хранение наборов изменений – позволит нам существенно сократить объем информации. И тонко контролировать их применение

Законченные версии файлов

Иногда во время работы мы будем "сохранять" наши изменения как законченные варианты

Такие "законченные версии" мы будем называть "коммиты"

Каждый коммит имеет: 
- Уникальное имя 

- Дату и время создания 

- Автора 

- Пояснительное сообщение: зачем его создавали 

- Набор изменений с момента прошлого коммита

Коммиты объединяются в ветки
![](01_git1.png)

Попробуем сделать наш пример с изменениями в git

- git init
	создает папку .git
	.git/ = папка, где будет храниться история изменений и мета-информация

У нас есть возможность смотреть информацию о состоянии проекта

- git log
	показывает список коммитов
	- хеш коммита
	- автор
	- дата
	- сообщение
- git status
	показывает на какой ветке находимся, никаких коммитов нет, есть файл mymodule но никак не участвует в git

Первая версия нашего файла mymodule.py 
```python
def my_function(first, second): 
	return first * second + 10
```

Создадим первый коммит

Каждый коммит имеет: 
- Уникальное имя: его git присвоит автоматически 
- Дату и время создания: она известна 
- Автора: я автор! Но кто я? 
- Пояснительное сообщение: мы его напишем 
- Набор изменений с прошлого коммита: мы их добавим

Итого, потребуется: 
- Единожды указать свои email и имя пользователя для git
- Пояснительное сообщение: мы его напишем 
- Набор изменений с момента прошлого коммита: мы их добавим

Единожды представимся 
```bash
git config --global user.name "Your Name" 
git config --global user.email "your@email"
```

Набор изменений, который мы еще не зафиксировали коммитом, называется staging

- git add
	фиксация изменений

- git commit
	делаем коммит с флагом -m сообщение 
	мета инфа 
	- файл создан 
	- сколько вставок

- git show [хеш]
	принимает хеш коммита и показывает всю информацию о нем

Внесем первое изменение 
```python
+++ def another_function(first): 
+++ return first + 1
```

- git diff
	показывает изменения относительно текущего коммита

Внесем второе изменение 
```python
+++# Previously I had some complex logic in this 
+++# module, but I had to delete it due to reasons. 
+++# Very sad!

def my_function(first, second):  
--- return first * second + 10 
+++ return first + second
```

- git checkout [хеш]
	переход по коммитам
	что показывает
	в состоянии detached HEAD
- git checkout -
	возвращает в момент из которого пришли 

___

Теперь поговорим про "распределенную" систему
backup

Нам нужно сохранять историю проекта где-то в интернете

github, gitlab, bitbucket

создание репозитория на хабе

- git remote
	показывает удаленный репозиторий
- git remote add [ссылка на \*.git на хабе]

Мы связали локальный проект с GitHub

Теперь, нужно синхронизировать изменения в них!

- git push origin master
	отправка на удаленный репозиторий
	origin - название удаленного репозитория
	master - ветка

На гитхабе мы можем добавить или поменять что-то

- git pull origin master
	вытягиваем изменения
	origin - название удаленного репозитория
	master - ветка

Полезности
- Можно скопировать репозиторий из сети
	- git clone
		копирует полностью весь репозиторий (ветки, коммиты, remote..)

- Файл .gitignore
	для хранения папок, путей, файлов, которые не нужны 

Онлайн курсы 
- https://git-school.github.io/visualizing-git/ (класс)

- https://learngitbranching.js.org/?locale=ru_RU (как пользоваться ветками)

- https://git-scm.com/doc (официальная)

- https://www.jetbrains.com/help/pycharm/using-gitintegration.html 

Выводы 
- Без истории изменений в нашем проекте – будет очень сложно работать 

- Хранить историю лучше всего как набор изменений в фиксированные точки времени жизни проекта 

- git позволяет удобно хранить историю нашего проекта 

- Его распределенная натура позволяет нам хранить историю сразу в нескольких местах и синхронизировать ее


Работа с git в команде

- git checkout
- git switch

git checkout работает 
- С номерами коммитов 
- С названиями веток

Состояние неопределенности или "detached HEAD"

переключаемся на какойто коммит
теперь находимся в состоянии "detached HEAD"
и не можем делать новые коммиты,
потому что программа не знает куда их присоединить в ветке
только на чтение
![](01_git2.png)

- git branch
	показывает текущую ветку master/main
	+==`[название ветки]`==. создаст новую ветку
	+флаг ==`-a`==. позволяет просмотреть все ветки

При создании ветки с помощью ==`git branch [название]`== создается идентичная ветка текущей ни на что не влияет

и при переключении веток с помощью ==`git checkout [название]`==
В другой ветке – мы можем вести разработку другой версии нашего кода!

Так можно делается для исправления багов, создания фич.

Что дает нам такое разделение? 
- В рамках одного проекта может быть несколько под-версий проекта 

- Изменения из одной ветки можно перетаскивать в другие 

- Работать в команде с ветками – намного удобнее

Какие ветки бывают?

- **Долгоживущие ветки**

![](01_git3.png)

Допустим ветка master/main и ветка version1. Для разных версий продукта
для разделения продакшн и теста

- **Одноразовые ветки**
Для правки бага и удаления
Если текущая 1 версия продукта и не надо долгоживущих изменения

![](01_git4.png)

- **Только одна ветка (Trunk Based Development)**
![](01_git5.png)

Сливать все в мастер. Для опытных 
+скорость разработки

Создадим уникальное изменения для новой ветки!

Новое изменение в ветку second
```python
+++ def new_function():
+++ print('I am new!')
```

Получим 
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return first + second 
	
def another_function(first):
	return first + 1 

def new_function(): 
	print('I am new')
```

git status
git add
git commit

git log

Проверим, что в master ничего не поменялось
git checkout master

Все осталось как было 
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad! 

def my_function(first, second): 
	return first + second 

def another_function(first):
	return first + 1
```

Теперь, внесем новое изменение в master!

Внесем второе изменение 
```python
def my_function(first, second): 
	--- return first * second + 10 
	+++ return 5
```

git add && git commit

git log
HEAD сдвинулся в master
локально master ушел дальше чем на github

```
git log --graph --decorate --all --oneline
```

Две версии кода
master
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return 5 

def another_function(first): 
	return first + 1
```

second
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return first + second 

def another_function(first):
	return first + 1 

def new_function(): 
	print('I am new')
```

получаем 2 несвязные ветки

Слияние веток

==`git merge [какую ветку в текущую] -m "..."`==

в master
`git merge second -m "Merging second into master"`
![](01_git6.png)

ветка second не изменилась, 
изменения из second засунули в master

Или можно использовать "git rebase"
отличаются

git rebase second
создастся новый коммит
и он привяжется к коммиту ветки second 
![](01_git7.png)

нет промежуточного коммита 
нет свободной ветки second (внутри master)
линейная ветка
позволяет делать историю коммитов более понятной

В чем разница? 
- "git merge" сохраняет ветвление, создает еще один дополнительный коммит.
	Более точное слияние, сохранение истории

- "git rebase" делает структуру плоской, не создает дополнительный коммит
	Более простая структура. Почти всегда используют 

Стала одна общая ветка
master
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad! 

def my_function(first, second): 
	return 5 
	
def another_function(first): 
	return first + 1 
	
def new_function(): 
	print('I am new')
```

А что если конфликт?

когда пытаемся перетянуть изменения из разных веток изменения к одному месту

git потребует, чтобы мы его разрешили

Варианты разрешения 
- Перезатри "мои" изменения "их" изменениями 

- Перезатри "их" изменения "моими" изменениями 

- Позволь мне руками сделать правильную версию из двух разных кусков
	наиболее распространена

Создадим конфликт!

- git checkout -b [название]
	создание ветки с переключением
	
![](01_git8.png)

Внесем третье изменение 
third 
```python
def my_function(first, second): 
--- return 5 6 
+++ return 5 + 1
```

Итого 
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return 5 + 1 

def another_function(first): 
	return first + 1 

def new_function(): 
	print('I am new')
```

git add && git commit

![](01_git9.png)
master остался

Теперь вернемся в master и сделаем что-нибудь противоположное
git checkout master

Внесем третье* изменение 
master
```python
def my_function(first, second): 
--- return 5 
+++ return 5 - 2
```

git add && git commit

![](01_git10.png)
git merge third 
conflict в файле

- git mergetool
	встроенный инструмент для разрешения конфликтов
	нежелательно пользоваться
	лучше пользоваться встроенным в IDE

выбраться что верно или свою логику

Теперь поправим конфликт

Стала одна общая 
master
```python
# Previously I had some complex logic in this 
# module, but I had to delete it due to reasons. 
# Very sad!

def my_function(first, second): 
	return 4

def another_function(first): 
	return first + 1 

def new_function(): 
	print('I am new')
```

git add && git commit
конфликт исправлен, ветка замержена
![](01_git11.png)

Полезности
- git pull --rebase
	в случает если наши обе ветки содержат разные коммиты и мы создали локальные коммиты, которых нет на удаленном репозитории и на удаленном репозитории есть коммиты которых нет локально, то эта команда превратит все в линейную ветку

если сделать просто git pull будет merge + commit
лучше все приводить в линейную историю
![](01_git12.png)

- git cherry-pick
	когда серьезно чтото пошло не так
	
	делали все на уровне веток но иногда это не нужно
	иногда из важно взять только 1 коммит
	пример:
	работали над большой фичей сделали много всего
	но оказалось что фича пока не нужна
	но одно изменение (коммит) оказалось важным 
	
	позволяет взять 1 коммит и использовать его.

git cherry-pick C3 C4 C7
![](01_git13.png)

другие коммиты не нужны а C3 C4 C7 нужны в master
вмерджит только эти коммиты правильным образом в master

теперь можно удалять ветки или замержить их после

- git revert
	создает новый коммит с отменой изменений из текущего коммита
	позволяет сохранить в истории изменения
	
	лучше делать так чем удалять коммит
![](01_git14.png)

- git config
	позволяет настроить name email
	поведение гита с внешними тулами

Без настроек
![](01_git15.png)

С правильными настройками
![](01_git16.png)

второй вариант намного приятнее и читабельнее 

https://github.com/sobolevn/dotfiles

Плагины

https://github.com/stevemao/awesome-git-addons

Хранение секретных файлов
https://github.com/sobolevn/git-secret


Дополнительные материалы

- https://stackoverflow.com/questions/57265785/whats-the-difference-between-git-switch-and-git-checkout-branch
	в чем разница git switch и git checkout
	
- https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified
	как отменять локальные изменения непросто git revert а взорвать коммит или уничтожить коммит и оставить изменения
	про git reset hard и soft
	
- https://www.atlassian.com/ru/git/tutorials/rewriting-history
	как переписывать локальную историю --amend
	перезапись коммита с новыми изменениями

Онлайн курсы

https://git-rebase.io/ про rebase например -i

- Для работы в команде – потребуется создавать ветки, чтобы удобно работать с несколькими версиями кода 

- В ветках могут быть конфликты, их бывает легко решить, а бывает – сложно 

- Вокруг git'а есть очень много удобных инструментов