# Домашнее задание к занятию «Уязвимости и атаки на информационные системы - Гнедин Максим»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  

Решение :
![открытые порты] (https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/img/1%20%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5.jpg)

1. Exploit for the 2.2 linux-kernel TCP/IP weakness (https://www.exploit-db.com/exploits/237)
2. Служба NFS (https://www.exploit-db.com/exploits/42305)
3. RPCBind (https://www.exploit-db.com/exploits/41974)




### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.*

Решение :

1. SYN - nmap -sS 192.168.133.130
   По протоколу TCP отправляется пакет с флагом ACK. Если что-то прослушивает порт, возвращается пакет с флагом SYN. ![скрин] (https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/img/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%202%20%D1%80%D0%B5%D0%B6%D0%B8%D0%BC%20SYN.jpg)
   Тогда для завершения отправляется пакет с RST. ![] (https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/img/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%202%20%D1%80%D0%B5%D0%B6%D0%B8%D0%BC%20SYN%202.jpg)
3. FIN - nmap -sA 192.168.133.130
   По протоколу TCP отправляет пакет с флагом FIN. Если нет ответа, то отображает информацию по порту. ![] (https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/img/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%202%20%D1%80%D0%B5%D0%B6%D0%B8%D0%BC%20FIN.jpg)
   Если пришёл ответ, порт в список не добавляется. ![] (https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/img/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%202%20%D1%80%D0%B5%D0%B6%D0%B8%D0%BC%20FIN%202.jpg)
5. Xmax - nmap -sX 192.168.133.130
   Ситуация примерно та же, что с FIN, только отпавляются три флага: FIN, PSH и URG. ![] (https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/img/XMAS.jpg)
6. UDP - nmap -sU 192.168.133.130
   Отличие этого метода можно обнаружить и без Wireshark – он медленный. Зато Wireshark помогает понять, почему – пакеты отправляются неколько раз. Другое заметное отличие – использование другого протокола и различие в виде запроса для некоторых портов.
   Порты помечаются как открытые (но фильтрующие), если после нескольких попыток ответ не пришёл.
Запишите сеансы сканирования в Wireshark. - https://github.com/maxgn87/sdb-homeworks-13-01/blob/main/paket.pcapng

   
