# Forge Emergency Services System

![Version](https://img.shields.io/badge/Version-1.0.0-blue.svg) 
![RocketMod](https://img.shields.io/badge/RocketMod-4.X-green.svg)
![Unturned](https://img.shields.io/badge/Unturned-3.X-yellow.svg)

## 📋 Содержание

- [Описание](#-описание)
- [Функциональные возможности](#-функциональные-возможности)
- [Установка](#-установка)
- [Настройка](#%EF%B8%8F-настройка)
  - [Основная конфигурация](#основная-конфигурация)
  - [Экстренные службы](#экстренные-службы)
- [Команды](#-команды)
- [Права доступа](#-права-доступа)
- [Интеграция с экономикой](#-интеграция-с-экономикой)
- [Руководство администратора](#-руководство-администратора)
- [Часто задаваемые вопросы](#-часто-задаваемые-вопросы)
- [Поддержка](#-поддержка)

## 🚨 Описание

**Forge Emergency Services System** - это комплексный плагин для Unturned, который добавляет реалистичную систему вызова и управления экстренными службами на вашем сервере. Плагин позволяет игрокам вызывать полицию, пожарную службу, скорую помощь и другие службы, а представителям этих служб - принимать вызовы, запрашивать поддержку и координировать действия.

Плагин идеально подходит для RP-серверов, добавляя глубину взаимодействия между службами и гражданами, создавая более реалистичную и захватывающую игровую среду.

## 🛠 Функциональные возможности

- **Система вызовов** - игроки могут вызывать экстренные службы, указывая причину вызова
- **Управление вызовами** - сотрудники служб могут принимать, передавать и завершать вызовы
- **Координация между службами** - возможность запрашивать поддержку других служб
- **Коммуникация** - внутрислужебная связь и общий канал для всех экстренных служб
- **Настраиваемые уведомления** - UI-интерфейс для отображения информации о вызове
- **Система защиты от троллинга** - временный бан для нарушителей, спамящих вызовами
- **Интеграция с экономикой** - оплата вызовов и вознаграждения для сотрудников
- **Маркеры на карте** - автоматическое отмечание места вызова для прибывших сотрудников

## 📥 Установка

1. Скачайте последнюю версию плагина из [официального источника]()
2. Распакуйте архив в папку `/Rocket/Plugins/` вашего сервера
3. Перезапустите сервер или загрузите плагин с помощью команды `/rocket load ForgeCallingEmergencyServices`
4. После первой загрузки плагин создаст файл конфигурации, который вы можете настроить

## ⚙️ Настройка

Конфигурационный файл находится по пути: `/Rocket/Plugins/ForgeCallingEmergencyServices/`

### Основная конфигурация

```xml
<?xml version="1.0" encoding="utf-8"?>
<Configuration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <EffectID>8888</EffectID>
  <EffectKey>888</EffectKey>
  <Cooldown>60</Cooldown>
  <EnableEconomy>false</EnableEconomy>
  <CallCost>100</CallCost>
  <ResponderReward>250</ResponderReward>
  <BlacklistDuration>30</BlacklistDuration>
  <BlacklistMaxViolations>3</BlacklistMaxViolations>
  <EnableSharedCommunication>true</EnableSharedCommunication>
  <EmergencyServices>
    <!-- Список служб находится здесь -->
  </EmergencyServices>
</Configuration>
```

| Параметр | Описание |
|----------|----------|
| `EffectID` | ID эффекта UI для отображения уведомлений |
| `EffectKey` | Ключ для UI эффекта |
| `Cooldown` | Время (в секундах) между вызовами от одного игрока |
| `EnableEconomy` | Включение/отключение экономической системы |
| `CallCost` | Стоимость вызова |
| `ResponderReward` | Награда сотруднику за принятие вызова |
| `BlacklistDuration` | Продолжительность блокировки вызовов (в минутах) |
| `BlacklistMaxViolations` | Максимальное количество нарушений до блокировки |
| `EnableSharedCommunication` | Разрешение общего канала связи между службами |

### Экстренные службы

```xml
<EmergencyServices>
  <Service id="1" name="Полиция" permission="forge.emergency.police" description="Нарушение закона или угроза безопасности" />
  <Service id="2" name="Пожарная служба" permission="forge.emergency.fire" description="Пожар или угроза возгорания" />
  <Service id="3" name="Скорая помощь" permission="forge.emergency.ambulance" description="Травма или неотложная медицинская помощь" />
</EmergencyServices>
```

| Атрибут | Описание |
|---------|----------|
| `id` | Уникальный ID службы (используется в командах) |
| `name` | Название службы |
| `permission` | Право доступа для сотрудников службы |
| `description` | Стандартное описание вызова для этой службы |

## 🔍 Команды

### Команды для гражданских лиц

| Команда | Синтаксис | Описание | Права |
|---------|-----------|----------|-------|
| `/call` | `/call <id/название> [описание]` | Вызвать экстренную службу | `forge.emergency.call` |
| `/emergencymsg` | `/emergencymsg <id вызова> <сообщение>` | Отправить сообщение участникам вызова | `forge.emergency.message` |

### Команды для сотрудников служб

| Команда | Синтаксис | Описание | Права |
|---------|-----------|----------|-------|
| `/acceptcall` | `/acceptcall <id>` | Принять вызов | `forge.emergency.accept` |
| `/supportcall` | `/supportcall <id вызова>` | Принять запрос поддержки | `forge.emergency.support` |
| `/completecall` | `/completecall <id>` | Завершить вызов | `forge.emergency.complete` |
| `/transfercall` | `/transfercall <id> <id службы/название службы>` | Передать вызов другой службе | `forge.emergency.transfer` |
| `/requestsupport` | `/requestsupport <id вызова> <id службы/название службы>` | Запросить поддержку другой службы | `forge.emergency.requestsupport` |
| `/servicemsg` | `/servicemsg <id службы/название службы> <сообщение>` | Отправить сообщение сотрудникам службы | `forge.emergency.servicemsg` |
| `/emergencybroadcast` | `/emergencybroadcast <сообщение>` | Отправить сообщение всем службам | `forge.emergency.broadcast` |

## 🔑 Права доступа

### Основные права

| Право | Описание |
|-------|----------|
| `forge.emergency.call` | Разрешает вызывать экстренные службы |
| `forge.emergency.message` | Разрешает отправлять сообщения участникам вызова |
| `forge.emergency.accept` | Разрешает принимать вызовы |
| `forge.emergency.support` | Разрешает принимать запросы поддержки |
| `forge.emergency.complete` | Разрешает завершать вызовы |
| `forge.emergency.transfer` | Разрешает передавать вызовы другим службам |
| `forge.emergency.requestsupport` | Разрешает запрашивать поддержку других служб |
| `forge.emergency.servicemsg` | Разрешает отправлять сообщения сотрудникам службы |
| `forge.emergency.broadcast` | Разрешает отправлять экстренные сообщения всем службам |

### Права для доступа к службам

| Право | Описание |
|-------|----------|
| `forge.emergency.police` | Доступ к функциям полиции |
| `forge.emergency.fire` | Доступ к функциям пожарной службы |
| `forge.emergency.ambulance` | Доступ к функциям скорой помощи |

## 💰 Интеграция с экономикой

Плагин поддерживает встроенную экономическую систему Unturned (опыт). Для активации этой функции:

1. Установите `EnableEconomy` в `true` в конфигурации
2. Настройте `CallCost` - стоимость вызова для игрока
3. Настройте `ResponderReward` - вознаграждение для сотрудника, принявшего вызов

```xml
<EnableEconomy>true</EnableEconomy>
<CallCost>100</CallCost>
<ResponderReward>250</ResponderReward>
```

## 👨‍💼 Руководство администратора

### Создание UI для плагина

1. Создайте UI эффект с необходимыми элементами:
   - Панель уведомлений (`NotificationPanel`)
   - Текстовые поля: `callIdText`, `callerText`, `serviceText`, `distanceText`, `timeText`, `descriptionText`
   - Кнопки: `acceptButton`, `declineButton`, `transferButton`, `supportButton`

2. Запишите ID эффекта и установите его в конфигурации.

### Управление экстренными службами

1. **Добавление новой службы**:
```xml
<Service id="4" name="Спасатели" permission="forge.emergency.rescue" description="Ситуации требующие спасения или эвакуации" />
```

2. **Настройка прав**:
   - Добавьте право доступа к службе в вашу систему разрешений (`Permissions.config.xml`)
   - Назначьте права нужным ролям/группам

### Анти-троллинг система

Система защиты от спама вызовами работает следующим образом:
- Игрок имеет ограниченное количество попыток (`BlacklistMaxViolations`)
- При отмене вызова (например, когда игрок вышел с сервера) счетчик нарушений увеличивается
- Когда количество нарушений достигает лимита, игрок попадает в черный список
- Черный список действует указанное в настройках время (`BlacklistDuration` минут)

## ❓ Часто задаваемые вопросы

**В: Совместим ли плагин с другими системами экономики?**

О: По умолчанию плагин использует встроенную систему опыта Unturned. Для интеграции с другими системами экономики может потребоваться модификация кода.

**В: Как настроить внешний вид UI?**

О: Вам необходимо создать UI с помощью редактора эффектов Unturned. Затем укажите ID эффекта в конфигурации плагина.

**В: Можно ли добавить больше экстренных служб?**

О: Да, вы можете добавить любое количество служб в конфигурационном файле, добавляя новые элементы `<Service>`.

**В: Как включить логирование вызовов?**

О: В текущей версии плагина нет встроенной системы логирования. Рассмотрите возможность использования плагинов логирования, совместимых с RocketMod.

## 🔧 Поддержка

Если у вас возникли проблемы с плагином:

1. Убедитесь, что вы используете последнюю версию плагина
2. Проверьте ваш конфигурационный файл на наличие ошибок
3. Проверьте, что все необходимые права доступа настроены правильно
4. При обнаружении ошибок, пожалуйста, создайте новый issue на GitHub

---

**Forge Emergency Services System** разработан для улучшения RP-игры на серверах Unturned. Если у вас есть предложения по улучшению плагина или вы обнаружили ошибку, пожалуйста, свяжитесь с разработчиками.

Made with ❤️ by Forge Team

---

_Документация обновлена: 31.03.2025_
