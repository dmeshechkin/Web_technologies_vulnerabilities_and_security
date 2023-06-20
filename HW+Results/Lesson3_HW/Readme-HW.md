1.Создать файл test.txt в корневом каталоге сервера. Получить этот файл через браузер.
- Установить в терминале программу curl, получить тот же файл с помощью этой программы.
- Установить telnet или netcat, получить тот же файл с помощью одной из этих программ.

2.Создать на сервере файл sensitive_info.txt. Добавить базовую HTTP авторизацию для этого файла.
- Получить этот файл через браузер.
- Получить тот же файл с помощью curl и telnet или netcat.

3. Открыть инструменты разработчика, вкладку Сеть (Network). Зайти на сайт https://geekbrains.ru. Проанализировать куки каждого запроса за HTML и картинками. Какие запросы уходят с куками, а какие без кук? Почему в каждом из случаев происходит именно такое поведение?

4. * Для выполнения этого задания вам потребуется:
1)Настроить домены attacker.com, sub.attacker.com, sub.sub.attacker.com, victim.com. Каждый из этих доменов должен указывать на 127.0.0.1
2)Настроить установку кук для доменов. Добавьте следюущий конфигурационный файл nginx (изменив root сервера на свой):
```
$ cat /etc/nginx/sites-available/cookie-research.conf
server {
listen 80;
server_name attacker.com;
root /var/www/html;

    location / {
     add_header "Set-Cookie" "test1=attacker-com_sub-attacker-com; Domain=sub.attacker.com";
            add_header "Set-Cookie" "test2=attacker-com_victim-com; Domain=victim.com";
            try_files $uri $uri/ =404;
    }
}

server {
listen 80;
server_name sub.attacker.com;
root /var/www/html;

    location / {
     add_header "Set-Cookie" "test3=sub-attacker-com_attacker-com; Domain=attacker.com";
            try_files $uri $uri/ =404;
    }
}

server {
listen 80;
server_name sub.sub.attacker.com;
root /var/www/html;

    location / {
     add_header "Set-Cookie" "test4=sub-sub-attacker-com_attacker-com; Domain=attacker.com";
            try_files $uri $uri/ =404;
    }
}
``
Проведите исследование механизма проставления кук, для этого попробуйте установить следующие куки:
1. С доменаattacker.comна доменsub.attacker.com
2. С доменаattacker.comна доменvictim.com
3. С доменаsub.attacker.comна доменattacker.com
4. С доменаsub.sub.attacker.comна доменattacker.com`
По каждому пункту ответьте на вопросы:
1. Куда установились куки?
2. Если не установились, то почему?
Обобщите полученные знания и напишите вывод в формате: "Домен может проставлять куки для себя, для ... и ..., но не может проставлять куки для ..., ... и ...".

5. (*) Сгенерировать самоподписанный сертификат и разместить его на своем сервере.