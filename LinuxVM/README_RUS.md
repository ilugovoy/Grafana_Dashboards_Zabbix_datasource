# Дашборд Grafana для мониторинга Linux-серверов через Zabbix

[![Grafana](https://img.shields.io/badge/Grafana-F2F4F9?style=for-the-badge&logo=grafana&logoColor=orange&labelColor=F2F4F9)](https://grafana.com) [![Zabbix](https://img.shields.io/badge/Zabbix-D50000?style=for-the-badge&logo=zabbix&logoColor=white)](https://www.zabbix.com) [![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.com/) 

Дашборд для визуализации метрик Linux-серверов, собираемых через Zabbix agent.

<!-- TOC tocDepth:2..3 chapterDepth:2..6 -->
- [Дашборд Grafana для мониторинга Linux-серверов через Zabbix](#дашборд-grafana-для-мониторинга-linux-серверов-через-zabbix)
  - [🖥️ Скриншоты интерфейса](#️-скриншоты-интерфейса)
  - [📊 Основные возможности](#-основные-возможности)
  - [🧩 Компоненты дашборда](#-компоненты-дашборда)
    - [Основные метрики](#основные-метрики)
    - [Секции дашборда](#секции-дашборда)
  - [⚙️ Требования к системе](#️-требования-к-системе)
  - [🚀 Установка](#-установка)
  - [🔧 Конфигурация Zabbix](#-конфигурация-zabbix)
  - [⚠️ Особенности реализации](#️-особенности-реализации)
  - [📄 Лицензия](#-лицензия)
<!-- /TOC -->

## 🖥️ Скриншоты интерфейса

![](./pics/new_linux.png)
![Секция 'DISC'](./pics/new_linux_disk.png)
![Секция 'NET'](./pics/new_linux_net.png)
![Секция 'CPU & RAM'](./pics/new_linux_cpuram.png)
![Секция 'History & Problems'](./pics/new_linux_problems.png)

## 📊 Основные возможности

- Мониторинг системных метрик в реальном времени
- Визуализация использования ресурсов: CPU, RAM, диски, сеть
- Отслеживание истории проблем и событий
- Автоматическое обнаружение сетевых интерфейсов и файловых систем
- Интеграция с Zabbix триггерами и оповещениями

## 🧩 Компоненты дашборда

### Основные метрики
- Время работы системы (Uptime)
- Версия Zabbix агента
- Время отклика ICMP

### Секции дашборда
**NET** - Сетевые интерфейсы
   - График трафика IN/OUT
   - Статистика по входящему и исходящему трафику
   
**DISC** - Дисковые системы
   - Использование пространства (%)
   - Общий объем дисков
   - Скорость чтения/записи
   
**CPU&RAM** - Процессор и память
   - График нагрузки CPU и RAM
   - Детализация времени CPU (системное/пользовательское)
   - Общая и используемая память
   
**History & Problems** - История проблем
   - Хронология событий
   - Сортировка по severity (Warning, Average, High)
   - Фильтрация по времени

## ⚙️ Требования к системе

1. **Zabbix Server** (версия 6.0+)
2. **Grafana** (версия 11.0+)
3. **Плагин Grafana для Zabbix** ([alexanderzobnin-zabbix-app](https://grafana.com/grafana/plugins/alexanderzobnin-zabbix-app/))
4. Linux-серверы с:
   - Zabbix Agent 2
   - сбором метрик через `Linux by Zabbix Agent`


## 🚀 Установка
1. Установите плагин Zabbix для Grafana по [инструкции](https://grafana.com/docs/plugins/alexanderzobnin-zabbix-app/latest/installation/) вендора
2. Настройте источник данных в Grafana:
    ```
    Тип: zabbix1-datasource
    URL: https://ваш_zabbix_сервер/api_jsonrpc.php
    ```
1. Импортируйте дашборд:
    ```
    В Grafana: `Create → Import → Upload JSON file`
    Выберите файл `Linux_Basic_Metrics.json`
    ```

## 🔧 Конфигурация Zabbix
Нужно добавить в шаблон айтем `Linux custom: Used memory [Ключ: memory.size(used)]` как показано на скриншоте:
![](./pics/for_memory_used_panel.png)

Обязательные элементы данных из шаблона `Linux by Zabbix Agent`  и `ICMP Ping`
```plaintext
Linux: System uptime
ICMP: ICMP response time
Linux: Version of Zabbix agent running
Network: Bits received/sent
Disk: Write/Read rate
Filesystem: Space utilization
CPU: System/User time
Memory: Total/Used memory
```

## ⚠️ Особенности реализации
- Дашборд содержит ссылки на дашборды `VM Windows` и `VMs TOP`
![](./pics/links.png)
- Для корректной работы всех панелей в Web-UI Zabbix нужно создать группу `Linux Servers`, включающую хосты, которые попадут в дашборд.
![](./pics/required_hostgroup_in_zabbix.png)

## 📄 Лицензия
Проект распространяется под лицензией [MIT](./LICENSE.txt)