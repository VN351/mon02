# Домашнее задание к занятию "13.Системы мониторинга"

## Обязательные задания

1. Вас пригласили настроить мониторинг на проект. На онбординге вам рассказали, что проект представляет из себя 
платформу для вычислений с выдачей текстовых отчетов, которые сохраняются на диск. Взаимодействие с платформой 
осуществляется по протоколу http. Также вам отметили, что вычисления загружают ЦПУ. Какой минимальный набор метрик вы
выведите в мониторинг и почему?
#
  Для проекта, который представляет собой платформу для вычислений с выдачей текстовых отчетов, минимальный набор метрик может включать:

    - Загрузка ЦПУ: Поскольку вычисления загружают ЦПУ, важно отслеживать его использование, чтобы определить, не перегружен ли сервер.

    - Время отклика HTTP: Это поможет понять, насколько быстро платформа отвечает на запросы.

    - Количество запросов: Позволяет отслеживать активность пользователей и нагрузку на систему.

    - Ошибки HTTP: Важно отслеживать ошибки, чтобы понять, как часто возникают проблемы с доступностью или функциональностью.

    - Использование памяти: Чтобы следить за потреблением ресурсов и избежать проблем с нехваткой памяти.

    - Свободное место на диске: Чтобы следить за колличеством свободного места на диске, чтобы избежать ситуации, когда система не сможет сохранить текстовые отчеты или временные файлы.

    - IOPS (операции ввода-вывода): Количество операций ввода-вывода в секунду. Этот параметр помогает оценить производительность дисковой подсистемы и определить, справляется ли она с текущей нагрузкой. Высокие значения IOPS могут указывать на интенсивное использование диска.

    - Время операций ввода-вывода (latency): Среднее время, которое требуется для выполнения операций чтения или записи на диск. Высокая задержка (latency) может свидетельствовать о проблемах с производительностью дисковой подсистемы или превышении ее возможностей.

    - Использование inode: Количество доступных inode на файловой системе. Inode — это структура данных, которая хранит информацию о файлах (например, их права доступа, владельца и местоположение на диске). Если inode заканчиваются, вы не сможете создавать новые файлы, даже если на диске есть свободное место. Это особенно важно для серверов, работающих с большим количеством мелких файлов. 

2. Менеджер продукта посмотрев на ваши метрики сказал, что ему непонятно что такое RAM/inodes/CPUla. Также он сказал, 
что хочет понимать, насколько мы выполняем свои обязанности перед клиентами и какое качество обслуживания. Что вы 
можете ему предложить?
#
  Если менеджеру продука не понятны термины RAM/inodes/CPUla, стоит ему объяснить их протыми словами:

    - RAM — это "временная рабочая зона" компьютера или сервера. Она используется для хранения данных и программ, которые активно используются в данный момент. Недостаток RAM может привести к медленной работе системы, задержкам в обработке запросов пользователей или даже к сбоям.

    - Inodes — это "каталог" файловой системы, который хранит информацию о каждом файле: его имя, размер, местоположение на диске и т.д. Если inodes заканчиваются, система не сможет создавать новые файлы. Это может привести к сбоям в работе приложений или невозможности записывать данные (например, логи).

    - CPU load average (CPUla) показывает, насколько загружен процессор вашего сервера. Это значение измеряет количество задач, которые процессор должен выполнять одновременно. Высокая загрузка CPU может привести к замедлению работы приложений и увеличению времени отклика для пользователей. Это может негативно сказаться на пользовательском опыте и бизнес-процессах.

  Для оценки выполнения обязательств перед клиентами и качества обслуживания можно предложить следующие метрики:

    - Service Level Agreement: Уровень выполнения соглашения по времени отклика и доступности.

    - Процент выполненных задач/запросов в срок: Доля задач/запросов, обработанных в рамках согласованных сроков

    - Net Promoter Score: Опрос пользователей о том, насколько они готовы рекомендовать продукт.

    - Аптайм: Процент времени, в течение которого ваш сервис был доступен клиентам

    - Количество инцидентов: Общее число сбоев или проблем в системе за определенный период.



 
3. Вашей DevOps команде в этом году не выделили финансирование на построение системы сбора логов. Разработчики в свою 
очередь хотят видеть все ошибки, которые выдают их приложения. Какое решение вы можете предпринять в этой ситуации, 
чтобы разработчики получали ошибки приложения?
#
  На построение системы сбора логов можно предложить использовать встроенные механизмы логирования приложений. Например:

    - Использовать стандартные механизмы логирования, такие как stdout или stderr, и настраивать их так, чтобы ошибки записывались в консоль.

    - Настроить простую систему уведомлений (например, через email или мессенджеры) при возникновении ошибок, используя существующие библиотеки логирования (например, log4j, winston).

    - Рассмотреть возможность использования бесплатных или open-source решений для сбора логов, таких как ELK Stack (Elasticsearch, Logstash, Kibana) или Grafana Loki.


4. Вы, как опытный SRE, сделали мониторинг, куда вывели отображения выполнения SLA=99% по http кодам ответов. 
Вычисляете этот параметр по следующей формуле: summ_2xx_requests/summ_all_requests. Данный параметр не поднимается выше 
70%, но при этом в вашей системе нет кодов ответа 5xx и 4xx. Где у вас ошибка?
#
  Существуют 5 категорий http-response. Информационный ответ (1ХХ), успешное выполнение (2ХХ), сообщения о перенаправлении (3ХХ), ошибка на стороне клиента (4ХХ), ошибка на стороне сервера (5ХХ). Если мы считаем успешным всё, что не 4ХХ и 5ХХ, то нужно использовать формулу: (summ_1xx_requests + summ_2xx_requests + summ_3xx_requests)/summ_all_requests.

5. Опишите основные плюсы и минусы pull и push систем мониторинга.
#
  ▎Pull-модель мониторинга
    В Pull-модели центральный сервер мониторинга периодически опрашивает (запрашивает) метрики у агентов или сервисов.
  ▎Плюсы Pull-модели:

    - Простота управления:  
      Централизованное управление сбором метрик на сервере мониторинга. Легко изменять частоту запросов, добавлять или удалять цели мониторинга без изменения конфигурации агентов.

    - Простота масштабирования:  
      Легко добавлять новые цели мониторинга, просто указав их на центральном сервере.

    - Автоматическое обнаружение проблем:  
      Если агент или сервис перестал отвечать, сервер мониторинга сразу узнает об этом, так как не сможет получить данные при следующем запросе.

    - Удобство реализации сервис-дискавери:  
      Удобно использовать автоматическое обнаружение новых сервисов (например, Kubernetes service discovery).

    - Безопасность:  
      Нет необходимости открывать дополнительные порты на агентах для отправки данных наружу. Данные запрашиваются сервером мониторинга, что позволяет лучше контролировать сетевые соединения и безопасность.

  ▎Минусы Pull-модели:

    - Сложность работы с кратковременными событиями:  
      Если событие произошло и исчезло между двумя запросами, оно может быть пропущено.

    - Проблемы с NAT и Firewall:  
      Сервер мониторинга должен иметь доступ к агентам, что иногда затруднено в сетях с NAT или строгими firewall-правилами.

    - Нагрузка на сервер мониторинга:  
      Сервер мониторинга должен самостоятельно опрашивать большое количество целей, что может создавать нагрузку на сеть и сервер.

---

  ▎Push-модель мониторинга

    В Push-модели агенты или сервисы сами отправляют (push) свои метрики на центральный сервер мониторинга.

  ▎Плюсы Push-модели:

    - Подходит для кратковременных событий:  
      Позволяет отправлять события сразу после их возникновения, что минимизирует вероятность пропуска важных данных.

    - Удобство работы в динамических окружениях:  
      Легко интегрировать с временными или динамическими средами (например, контейнеры, serverless), где серверу мониторинга сложно постоянно отслеживать наличие новых объектов.

    - Удобство работы с NAT и Firewall:  
      Агент инициирует соединение сам, что упрощает прохождение через NAT и firewall.

    - Гибкость отправки данных:  
      Агент может отправлять данные по мере их появления или пакетами в удобное время (например, при низкой нагрузке).

  ▎Минусы Push-модели:

    - Отсутствие встроенного контроля доступности агентов:  
      Если агент перестал отправлять данные, сервер мониторинга не всегда сразу заметит это (необходимы дополнительные механизмы контроля).

    - Безопасность и управление доступом:  
      Сервер должен принимать входящие соединения от множества агентов. Это требует более сложной настройки безопасности и управления доступом.

    - Сложность масштабирования конфигурации агентов:  
      При изменении параметров сбора метрик необходимо менять конфигурацию каждого агента отдельно, что может быть неудобно при большом количестве агентов.


6. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

    - Prometheus 
    - TICK
    - Zabbix
    - VictoriaMetrics
    - Nagios
#
  - Prometheus  
    Pull (основная модель), но есть возможность использовать и Push через дополнительный компонент — Pushgateway.  
  
  Итог: Pull (основная), но возможен гибридный подход.

  - TICK stack (Telegraf, InfluxDB, Chronograf, Kapacitor)    
    - Telegraf собирает и отправляет данные в InfluxDB (Push).  
    - InfluxDB принимает входящие данные (Push).  
    - Kapacitor может как получать данные из InfluxDB, так и принимать напрямую от агентов (Push).  
  Итог: Push-модель.

  - Zabbix  
    - Zabbix-агенты могут работать в активном режиме (Push) и пассивном режиме (Pull).  
    - Также можно использовать SNMP, IPMI и другие протоколы с Pull-подходом.  
  Итог: Гибридная модель.

  - VictoriaMetrics  
    - Совместима с протоколом Prometheus и может выполнять Pull-запросы (как Prometheus).  
    - Также поддерживает прием данных по Push-протоколам (например, через Remote Write API).  
  Итог: Гибридная модель.

  - Nagios  
    В основном Pull-модель, но также может использовать Push через дополнения (например, NRDP, NSCA).  
  Итог: Pull (основная), но возможен гибридный подход.

7. Склонируйте себе [репозиторий](https://github.com/influxdata/sandbox/tree/master) и запустите TICK-стэк, 
используя технологии docker и docker-compose.

В виде решения на это упражнение приведите скриншот веб-интерфейса ПО chronograf (`http://localhost:8888`). 

P.S.: если при запуске некоторые контейнеры будут падать с ошибкой - проставьте им режим `Z`, например
`./data:/var/lib:Z`
#
![alt text](https://github.com/VN351/mon02/raw/main/images/1-1.jpg)
![alt text](https://github.com/VN351/mon02/raw/main/images/1-22.jpg)


8. Перейдите в веб-интерфейс Chronograf (http://localhost:8888) и откройте вкладку Data explorer.
        
    - Нажмите на кнопку Add a query
    - Изучите вывод интерфейса и выберите БД telegraf.autogen
    - В `measurments` выберите cpu->host->telegraf-getting-started, а в `fields` выберите usage_system. Внизу появится график утилизации cpu.
    - Вверху вы можете увидеть запрос, аналогичный SQL-синтаксису. Поэкспериментируйте с запросом, попробуйте изменить группировку и интервал наблюдений.

Для выполнения задания приведите скриншот с отображением метрик утилизации cpu из веб-интерфейса.
#
![alt text](https://github.com/VN351/mon02/raw/main/images/2-1.jpeg)

9. Изучите список [telegraf inputs](https://github.com/influxdata/telegraf/tree/master/plugins/inputs). 
Добавьте в конфигурацию telegraf следующий плагин - [docker](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/docker):
```
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```

Дополнительно вам может потребоваться донастройка контейнера telegraf в `docker-compose.yml` дополнительного volume и 
режима privileged:
```
  telegraf:
    image: telegraf:1.4.0
    privileged: true
    volumes:
      - ./etc/telegraf.conf:/etc/telegraf/telegraf.conf:Z
      - /var/run/docker.sock:/var/run/docker.sock:Z
    links:
      - influxdb
    ports:
      - "8092:8092/udp"
      - "8094:8094"
      - "8125:8125/udp"
```

После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список `measurments` в 
веб-интерфейсе базы telegraf.autogen . Там должны появиться метрики, связанные с docker.

Факультативно можете изучить какие метрики собирает telegraf после выполнения данного задания.

![alt text](https://github.com/VN351/mon02/raw/main/images/3-1.jpeg)

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

1. Вы устроились на работу в стартап. На данный момент у вас нет возможности развернуть полноценную систему 
мониторинга, и вы решили самостоятельно написать простой python3-скрипт для сбора основных метрик сервера. Вы, как 
опытный системный-администратор, знаете, что системная информация сервера лежит в директории `/proc`. 
Также, вы знаете, что в системе Linux есть  планировщик задач cron, который может запускать задачи по расписанию.

Суммировав все, вы спроектировали приложение, которое:
- является python3 скриптом
- собирает метрики из папки `/proc`
- складывает метрики в файл 'YY-MM-DD-awesome-monitoring.log' в директорию /var/log 
(YY - год, MM - месяц, DD - день)
- каждый сбор метрик складывается в виде json-строки, в виде:
  + timestamp (временная метка, int, unixtimestamp)
  + metric_1 (метрика 1)
  + metric_2 (метрика 2)
  
     ...
     
  + metric_N (метрика N)
  
- сбор метрик происходит каждую 1 минуту по cron-расписанию

Для успешного выполнения задания нужно привести:

а) работающий код python3-скрипта,

б) конфигурацию cron-расписания,

в) пример верно сформированного 'YY-MM-DD-awesome-monitoring.log', имеющий не менее 5 записей,

P.S.: количество собираемых метрик должно быть не менее 4-х.
P.P.S.: по желанию можно себя не ограничивать только сбором метрик из `/proc`.

2. В веб-интерфейсе откройте вкладку `Dashboards`. Попробуйте создать свой dashboard с отображением:

    - утилизации ЦПУ
    - количества использованного RAM
    - утилизации пространства на дисках
    - количество поднятых контейнеров
    - аптайм
    - ...
    - фантазируйте)
    
    ---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

