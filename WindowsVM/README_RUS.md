# Дашборд Grafana для мониторинга Windows-серверов через Zabbix

[![Grafana](https://img.shields.io/badge/Grafana-F2F4F9?style=for-the-badge&logo=grafana&logoColor=orange&labelColor=F2F4F9)](https://grafana.com) [![Zabbix](https://img.shields.io/badge/Zabbix-D50000?style=for-the-badge&logo=zabbix&logoColor=white)](https://www.zabbix.com) [![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://www.microsoft.com/) 

Дашборд для визуализации метрик Windows-хостов, собираемых через Zabbix agent.

<!-- TOC tocDepth:2..3 chapterDepth:2..6 -->
- [Дашборд Grafana для мониторинга Windows-серверов через Zabbix](#дашборд-grafana-для-мониторинга-windows-серверов-через-zabbix)
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

![](./pics/new_windows.png)
![Секция 'DISC'](./pics/new_windows_disk.png)
![Секция 'NET'](./pics/new_windows_net.png)
![Секция 'CPU & RAM'](./pics/new_windows_cpuram.png)
![Секция 'History & Problems'](./pics/new_windows_problems.png)

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
4. Windows-хосты с:
   - Zabbix Agent 2
   - сбором метрик через `Windows by Zabbix Agent`


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
    Выберите файл `Windows_Basic_Metrics.json`
    ```

## 🔧 Конфигурация Zabbix

Обязательные элементы данных из шаблонов `Windows by Zabbix Agent` и `ICMP Ping`
```plaintext
Windows: Uptime
Disk: Write/Read rate
CPU: System/User time
ICMP: ICMP response time
Memory: Total/Used memory
Network: Bits received/sent
Filesystem: Space utilization
Windows: Version of Zabbix agent running
```

## ⚠️ Особенности реализации
- Дашборд содержит ссылки на дашборды `VM Linux` и `VMs TOP`
![](./pics/links.png)
- Для корректной работы всех панелей в Web-UI Zabbix нужно создать группу `Linux Servers`, включающую хосты, которые попадут в дашборд.
![](./pics/required_hostgroup_in_zabbix.png)

## 📄 Лицензия
Проект распространяется под лицензией [MIT](./LICENSE.txt)