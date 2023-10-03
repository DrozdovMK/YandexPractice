# Шпаргалка по Git
# Часть 1. Основные концепции.
---
### 1. Что такое Git

Git - система контроля версий создаваемого приложения/программы и т.д. Она нужна для того, чтобы откатить изменения, 
когда ты натворил что-то плохое или просто запутался в своем же коде.

### 2. Концепция работы с локальным репозиторием.

В процессе работы с Git ты делаешь несколько простых шагов, которые облегчают тебе жизнь. Первым делом ты определяешь папку, в которой 
будут храниться файлы, в этой папке теперь будет царить порядок. Чтобы дать понять Git, что мы хотим следить за папкой, нужно *инициализировать репозиторий*.

```bash
cd <путь до нужной папки>
git init
```

После инициализации мы имеем возможность следить за изменениями файлов, находящихся в репозитории. Например, если как-то поменять любой файл из репозитория, то
Git заметит это и при вызове команды git status даст нам знать. Применение команды git add "Имя файла" (Возможно к разным файлам) мы даем понять гиту, что 
изменения этих файлов нас устраивают и в дальнейшем мы из "закоммитим", то есть поставим контрольную точку, к которой в дальнейшем сможем откатиться. Коммит осуществляется
командой git commit -m "Текст заметки, чтобы легче было ориентроваться по коммитам в дальнейшем". Таким образом изменив файл text.txt из репозитория закоммитить его можно так:

```bash
git add text.txt
git commit -m "Первое изменение первого файла"
```

### 3. Концепция работы с удаленным репозиторем.

* Git позвояет также создавать удаленные репозитории,чтобы проводить работу над совместными проектами. Для связи локального и удаленного репозитория 
вам нужно сгенерировать пару SSH-ключей. Это можно сделать с помощью команды ssh-keygen. Эта команда создаст приватный и публичный ключи, которые будут 
использоваться для аутентификации. 

* После генерации ключей, нужно будет добавить содержимое ключа id_rsa.pub на удаленный сервер (например это страничка репозитория в гитхабе)

* Потом нужно свзать локальный и удаленный репозиторий командой git remote add origin <URL>, где <URL> - это URL-адрес удаленного репозитория. 
Это устанавливает связь между локальным и удаленным репозиториями и присваивает им имя origin.

* Ну и наконец чтобы послать коммит из локального репозитория на удаленный, нужно использовать git push origin <branch>, где <branch> - это имя ветки, в которую вы хотите 
отправить изменения. Эта команда загружает ваши локальные изменения в удаленный репозиторий.
---

Таким образом, получаем хороший инструмент контроля версий, который полезно использовать как одному, так и в команде))

---
# Часть 2. Хэши, логи, HEAD, статусы файлов, обращение к коммитам

### 1. Хэши.

Команда git log позволяет вывести историю всех коммитов (чекпоинтов). Рядом со словом commit справа будет непонятный набор цифр. Это хэш, который содержит зашифрованную 
информацию о коммите.Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. 
Можно сказать, что хеш — основной идентификатор коммита. 

Команда git log --oneline позволит вывести сокращенный лог, который все также содержит всю информацию о коммите, только используя меньше символов, это легче читается.

### 2. HEAD.

При вызове команды git log также есть надпись (HEAD -> master) после хеша одного из коммитов.
Файл HEAD — один из служебных файлов папки .git. Он указывает на коммит, который сделан последним (то есть на самый новый). После очередного коммита HEAD обновляется.
Многие команды Git принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно просто написать слово HEAD — Git поймёт,
что вы имели в виду последний коммит.