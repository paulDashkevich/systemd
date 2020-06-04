# systemd
# ДЗ по systemd, пункт 1. (inline скрипт в файле Вагрант)
* 1.1 Создаём сервис в /etc/systemd/system/check30sec.service
* 1.2 Создаём таймер /etc/systemd/system/check30sec.timer
* 1.3 Создаём лог и ключевое слово в /etc/sysconfig
```sh
systemd: NEXT                         LEFT       LAST PASSED UNIT                         ACTIVATES
systemd: Mon 2020-06-01 05:58:14 UTC  29s left   n/a  n/a    checklog.timer               checklog.service

systemd: Jun  1 05:57:44 localhost root: Mon Jun 1 05:57:44 UTC 2020: I found the word:ALERT!
systemd: Jun  1 05:57:44 localhost systemd: Started My log check service.
systemd: Jun  1 05:57:44 localhost systemd: Started Timer checklog every 30s.
systemd: Jun  1 05:57:44 localhost systemd: Starting Timer checklog every 30s.
```


# ДЗ по systemd, пункт 2. (inline скрипт в файле Вагрант)
* 2.1 Устанавливаем spawn-fcgi
* 2.2 В конфиге убираем комментирование строк SOCKET OPTIONS
* 2.3 Создаём unit-file   cat /etc/systemd/system/spawn-fcgi.service
* 2.4 Релоадим демона systemd, стартуем и чекаем статус
```sh
    systemd: ● spawn-fcgi.service - Spawn FastCGI service
    systemd:    Loaded: loaded (/etc/systemd/system/spawn-fcgi.service; disabled; vendor preset: disabled)
    systemd:    Active: active (running) since Mon 2020-06-01 05:55:36 UTC; 82ms ago
    systemd:  Main PID: 3329 (php-cgi)
    systemd:    CGroup: /system.slice/spawn-fcgi.service
    systemd:            ├─3329 /usr/bin/php-cgi
    systemd:            ├─3330 /usr/bin/php-cgi
    systemd:            ├─3331 /usr/bin/php-cgi
    systemd:            ├─3332 /usr/bin/php-cgi
    systemd:            ├─3333 /usr/bin/php-cgi
    systemd:            ├─3334 /usr/bin/php-cgi
    systemd:            ├─3335 /usr/bin/php-cgi
    systemd:            ├─3336 /usr/bin/php-cgi
    systemd:            ├─3337 /usr/bin/php-cgi
    systemd:            ├─3338 /usr/bin/php-cgi
    systemd:            ├─3339 /usr/bin/php-cgi
    systemd:            ├─3340 /usr/bin/php-cgi
    systemd:            ├─3341 /usr/bin/php-cgi
    systemd:            ├─3342 /usr/bin/php-cgi
    systemd:            ├─3343 /usr/bin/php-cgi
    systemd:            ├─3344 /usr/bin/php-cgi
    systemd:            ├─3345 /usr/bin/php-cgi
    systemd:            ├─3346 /usr/bin/php-cgi
    systemd:            ├─3347 /usr/bin/php-cgi
    systemd:            ├─3348 /usr/bin/php-cgi
    systemd:            ├─3349 /usr/bin/php-cgi
    systemd:            ├─3350 /usr/bin/php-cgi
    systemd:            ├─3351 /usr/bin/php-cgi
    systemd:            ├─3352 /usr/bin/php-cgi
    systemd:            ├─3353 /usr/bin/php-cgi
    systemd:            ├─3354 /usr/bin/php-cgi
    systemd:            ├─3355 /usr/bin/php-cgi
    systemd:            ├─3356 /usr/bin/php-cgi
    systemd:            ├─3357 /usr/bin/php-cgi
    systemd:            ├─3358 /usr/bin/php-cgi
    systemd:            ├─3359 /usr/bin/php-cgi
    systemd:            ├─3360 /usr/bin/php-cgi
    systemd:            └─3361 /usr/bin/php-cgi
    systemd:
    systemd: Jun 01 05:55:36 systemd systemd[1]: Started Spawn FastCGI service.
    systemd: Jun 01 05:55:36 systemd systemd[1]: Starting Spawn FastCGI service...
```
# ДЗ по systemd, пункт 3. (inline скрипт в файле Вагрант)
* 3.1 Устанавливаем httpd
* 3.2 Создаём unit-шаблон для последующих инстансов
* 3.3 Создаём конфиги для каждого следующего клона шаблона @
* 3.4 Для каждого клона создаём свой pid-файл и меняем стандартный порт апача на отличный от 80-порта, в данном случае: 8008, 8009
* 3.5 Слушаем порты и видим работу скрипта:
```
    systemd: tcp    LISTEN     0      128      :::8008                 :::*                   users:(("httpd",pid=3266,fd=4),("httpd",pid=3265,fd=4),("httpd",pid=3264,fd=4),("httpd",pid=3263,fd=4),("httpd",pid=3262,fd=4),("httpd",pid=3260,fd=4))
    systemd: tcp    LISTEN     0      128      :::8009                 :::*                   users:(("httpd",pid=3272,fd=4),("httpd",pid=3271,fd=4),("httpd",pid=3270,fd=4),("httpd",pid=3269,fd=4),("httpd",pid=3268,fd=4),("httpd",pid=3267,fd=4))
```
