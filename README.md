# Домашнее задание к занятию «Защита сети» Тимахова Наталья

# Задание 1

![atakisvm2](https://github.com/timakhova/13-03netprotection/blob/main/1-%D0%B0%D1%82%D0%B0%D0%BA%D0%B8-%D1%81-%D0%B2%D0%BC2.png)
![logivm1](https://github.com/timakhova/13-03netprotection/blob/main/1-%D0%BB%D0%BE%D0%B3%D0%B8.png)
![zaprosfake2ban](https://github.com/timakhova/13-03netprotection/blob/main/1-%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81%D1%84%D1%8D%D0%B9%D0%BA2%D0%B1%D0%B0%D0%BD.png)
![logsfake2ban](https://github.com/timakhova/13-03netprotection/blob/main/1-%D0%BB%D0%BE%D0%B3%D1%84%D1%8D%D0%B9%D0%BB2%D0%B1%D1%8D%D0%BD.png)

### **Общие выводы**
1. **Suricata срабатывает на сетевые атаки и сканирование портов**, благодаря встроенным правилам из Emerging Threats (ET). Это указывает на корректную настройку IDS (Intrusion Detection System).
2. **Типы событий**:
   - **DROP (Spamhaus, Dshield, CINS)**: Эти события означают, что трафик поступает от IP-адресов с плохой репутацией (в чёрных списках). Такие IP часто используются для атак, спама или других злонамеренных действий.
   - **SCANS (Suspicious inbound)**: Указывает на попытки сканирования открытых портов на вашей системе. Это может быть подготовка к атаке.

---

### **Ключевые события**

#### 1. **DROP события (Spamhaus, Dshield, CINS Active Threat Intelligence)**
   Пример:
   ```plaintext
   11/17/2024-16:01:48.101569  [**] [1:2400012:4163] ET DROP Spamhaus DROP Listed Traffic Inbound group 13 [**] [Classification: Misc Attack] [Priority: 2] {TCP} 91.240.118.248:57593 -> 10.131.0.13:33572
   ```
   - **Spamhaus DROP Listed Traffic**: IP `91.240.118.248` включён в чёрный список Spamhaus. Это означает, что данный источник был замечен в подозрительных или злонамеренных действиях.
   - **Порт назначения (10.131.0.13:33572)**: Система пыталась подключиться к указанному порту на VM1.

   Рекомендуется заблокировать такие IP на уровне firewall, если это возможно.

---

#### 2. **SCANS (Подозрительное сканирование портов)**
   Пример:
   ```plaintext
   11/17/2024-16:04:08.260701  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 84.201.180.161:44314 -> 10.131.0.13:3306
   ```
   - **Мишени для сканирования**:
     - **MySQL (порт 3306)**
     - **MSSQL (порт 1433)**
     - **PostgreSQL (порт 5432)**
     - **Oracle SQL (порт 1521)**
     - **VNC (порты 5900-5920 и 5800-5820)**

   Эти события указывают на попытки найти открытые порты баз данных и других сервисов для последующего взлома.

---

#### 3. **Приоритет и классификация**
   - **Priority: 2**: Средний уровень угрозы. Эти события требуют внимания, но не всегда свидетельствуют о прямой атаке.
   - **Classification**:
     - `Misc Attack`: Общая категория для подозрительных действий.
     - `Potentially Bad Traffic`: Потенциально вредоносный трафик, например, попытки сканирования или тестирования уязвимостей.
     - `Attempted Information Leak`: Попытка сбора информации о системе.

# Задание 2




