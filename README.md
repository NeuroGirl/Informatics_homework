# Лабораторная работа: планировщик задач сron

Планировщик задач cron используется для автоматизации выполнения скриптов. Обычно его применяют для регулярного резервного копирования данных, перезагрузки сервера и других не требующих пристального внимания человека задач. Сегодня мы познакомимся с основами его ипользования.

## Пример (его в отчет включать не нужно)

### 1. Создаем файл для исполнения

  Для того, чтобы увидеть работу cron на практике, нам нужен файл, который мы непосредственно будем регулярно выполнять. Пусть, для примера, это будет файл с именем `script.bash` со следующим содержимым:
  
   ```
   echo "hello"
   ```

  Не забудьте сделать этот файл исполняемым с помощью команды: 

   ```
   chmod +x script.bash
   ```

### 2. Создаем и открываем crontab файл (в нем и прописывается код для исполнения скриптов)
   
   ```
   crontab -e
   ```

   Скорее всего ранее на вашей машине не было ни одного crontab файла, поэтому когда мы в первый раз применяем описанную выше команду, терминал сообщит об этом и попросит вас выбрать редактор crontab файлов, чтобы создать и открыть ваш первый crontab файл именно в нем. Чаще всего выбирают nano. Впоследствие все crontab файлы будут открываться именно выбранным редактором.

### 3. Прописываем скрипт в открытом файле crontab

   Записываем в открытый нами файл следующий код:

   ```
   * * * * * /путь_к_файлу/script.bash >> /home/ubuntu/script.log 2>&1
   ```

   Поясню каждую из частей кода: 
   
   - Первые пять * отвечают за настройку времени врегулярного исполнения скрипта. Первая - за минуты (например 34 * * * * будет значить, что файл будет исполняться каждый час в 34-ую его минуту: в 14.34, 15.34 и т.д.), вторая - за часы (34 5 * * * будет значить, что файл будет исполняться каждый день в 5.34 утра), третья - за день месяца (34 5 8 * * - файл исполняется 8-ого числа каждого месяца в 5.34 утра), четвертая - за месяц (34 5 8 1 * - файл исполняется каждый год 8-ого января в 5.34 утра) и послядняя - за день недели (34 5 * * 1 - файл исполняется в 5.34 каждый понедельник). Знак * собирает в себе все возможные значения конкретного параметра.  
   - `/путь_к_файлу/script.bash` - соответсвенно обозначает путь к созданному нами ранее файлу script.bash. Именно здесь мы указываем, кто crontab должен исполнять именно его.
   - `/home/ubuntu/script.log 2>&1` - обычно cron направляет вывод скриптов на почту пользователя, если она указана в памяти машины, что может усложнить просмотр итогов выполнения программы. Чтобы этого избеджать, перенаправим результат исполнения программы в файл script.log. Отдельно создавать его не нужно, он создатся сам.

   Сохраняем изменения в файле с помощью Ctrl + S и закрываем файл с помощью Ctrl + X.

### 4. Ждем несколько минут и смотрим на результат

   Если все сделано корректно, открыв файл `script.log` несколько минут мы обнаружим в нем несколько строчек с надписью "hello", их количество будет зависеть от количества прошедшего времени.

## :red_circle: Задание (включаем в отчет!)





   
