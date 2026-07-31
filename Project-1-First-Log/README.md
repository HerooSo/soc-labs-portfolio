# Проект 1: Обнаружение SSH-брутфорса

**Аналитик:** Сергей 
**Дата:** 31 июля 2026 г. 
**Статус:** Завершено

---

## Цель

Научиться анализировать системные логи и обнаруживать признаки атаки перебором паролей (Brute Force) по SSH.

---

## Среда

- **ОС жертвы:** Ubuntu Server 26.04 LTS
- **Атакующий:** Windows 10 (хостовая машина)
- **Лог-файл:** `/var/log/auth.log`

---

## Результаты анализа

### 1. Неудачные попытки входа (Failed password)

**Команда:**
```bash
sudo cat /var/log/auth.log | grep "Failed password" | tail -5

**Результат:**
2026-07-31T06:55:43.952544+03:00 sergey-VMware-Virtual-Platform sshd-session[6379]: Failed password for sergey from 192.168.231.136 port 39254 ssh2
2026-07-31T06:55:49.445688+03:00 sergey-VMware-Virtual-Platform sshd-session[6379]: Failed password for sergey from 192.168.231.136 port 39254 ssh2
2026-07-31T06:55:53.062410+03:00 sergey-VMware-Virtual-Platform sshd-session[6379]: Failed password for sergey from 192.168.231.136 port 39254 ssh2

**Статистика:**
- **Всего попыток:** 5
- **Ip атакующего:** 127.0.0.1 ; 192.168.231.136
- **Целевой пользователь:** sergey

### 2. Удачные попытки входа (Accepted password)

**Команда:**
```bash
sudo cat /var/log/auth.log | grep "Accepted password"

**Результат:**
2026-07-31T06:51:19.780716+03:00 sergey-VMware-Virtual-Platform sshd-session[5765]: Accepted password for sergey from 127.0.0.1 port 34618 ssh2

---

## Вывод

-[x] Атака обнаружена по записи "Failed password".
-[x] Зафиксирован успешный вход после неудачных атак.
-[x] Логи /var/log/auth.log содержать всю информацию для расследования.

---

## Рекомендации

- **Настроить fail2ban для автоматической блокировки IP.
- **Использовать сложные пароли.**
- **Настроить отправку логов в SIEM для централизованного мониторинга.**
- **Включить 2FA для SSH-доступа**
