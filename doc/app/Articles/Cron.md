# Описание настройки и использования CRON

### План
1. О контейнере
2. Настройка крон заданий
3. Проверка заданий
4. Материалы

### 1. О контейнере

Для установки CRON в докер используется планировщик задач для крон - Ofelia (`mcuadros/ofelia`)

Ofelia - это современный и малозатратный планировщик заданий для сред docker, построенный на `Go`. 
Офелия стремится стать заменой старомодному cron.

### 2. Настройка крон заданий

Расписания заданий лежит в файле `config/docker/cron/config.ini`

Надо учитывать момент что расписание задач выставляется немного подругому чем в привычном `crontab`. 
Подробности по синтаксису расписания можно посмотреть по ссылкам в материалах, а таже в шапке конфига (краткая информация)

### 3. Проверка заданий

Чтобы добавить новое задание, 
 - Откройте файл `config/docker/cron/config.ini`
 - Добавьте туда новое задание
 - Остановите контейнер крон командой `mic cron stop`
 - Запустите контейнер крон командой `mic cron start`
 - После этого все задания должны перезапуститься согласно графику

Иметь ввиду, что в классическом варианте расписаний задания запускаются в начале 
временного периода (в начале часа, в начале минуты и т д), потому при перезапуске контейнера, 
задания могут запускаться не сразу

Задания прописывать учитывая названия контейнера в каком будет оно запускаться. 
Примеры есть в конфиге, а также читать в материалах

После запуска требуемого задания можно проверить результат выполнения команды, которая запускалась этим заданием

Лайфхак: Чтобы наглядно проконтролировать запуск задач, можно задачи запускать используя `pm2` легкая и мощная 
служба мониторинга, которая выдает статистику. Так можно отследить задачи которые запущены в фоновом режиме
Пример команды расписания, используя `pm2`:

`command = "pm2 start 'bin/console rabbitmq:consumer telegram_notification -vvv'"`

После старта задачи, для того чтобы увидет запущенную задачу, нужно зайти в контейнер приложения `mic s` 
и открыть средство мониторинга pm2 командой `sudo pm2 monit`, 
либо просто список запущенных через pm2 фоновых программ `sudo pm2 list`

### 4. Материалы

1. Официальный репозиторий и документация для mcuadros/ofelia
https://github.com/mcuadros/ofelia
2. Статья о настройке заданий для Ofelia
https://php.dragomano.ru/docker-dlja-lokalnoj-veb-razrabotki-chast-8
3. Еще статья по настройке задач
https://pkg.go.dev/github.com/robfig/cron#section-sourcefiles			