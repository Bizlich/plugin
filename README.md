## RustApp Plugin
Для того, чтобы полноценно пользоваться сервисом RustApp, вам необходимо установить этот плагин и не забывать следить за его обновлениями. Это важно!

## 🔗 Integrations

<details><summary>Личные сообщения</summary>

   <br>Сервис может показывать и хранить личные переписки ваших игроков через `/pm` и `/r`, но для этого вам необходимо научить их работать вместе.

   ```csharp
   plugins.Find("RustApp")?.Call("RA_DirectMessageHandler", senderId, targetId, message);
   ```
   `senderId` - String SteamID64 отправителя\
   `targetId` - String SteamID64 получателя\
   `message` - текст сообщения<br>
   
</details>

<details><summary>Репорты из своей системы</summary>

   <br>Для отправки репортов в RustApp можно использовать и свою систему жалоб, но для этого необходимо связать свой плагин с плагином RustApp.
   
   ```csharp
   plugins.Find("RustApp")?.Call("RA_ReportSend", initiatorId, targetID, reason, <optional> message)
   ```
   `senderId` - String SteamID64 того, кто жалуется\
   `targetId` - String SteamID64 того, на кого жалуются\
   `reason` - причина жалобы (читы/макросы и т.д)\
   `message` - комментарий к репорту (можно не передавать, если Ваш плагин не поддерживает комментарии к жалобам)

   ⚠️ Не забудьте из конфигурации `RustApp.json` убрать все команды, чтобы наше UI нельзя было открыть!

</details>

<details><summary>Собственные оповещения [тариф Pro]</summary>

   <br>Вы можете создавать свои собственные оповещения о любых действиях игрока при помощи API.
   
   ```csharp
   plugins.Find("RustApp")?.Call("RA_CustomAlert", message, <optional> data)
   ```
   `message` - любая произвольная строка\
   `data` - любой JSON с нужной вам информацией (кол-во символов не более 512), который будет также отображаться на сайте

   ⚠️ Если в `message` будет содержаться SteamID - на сайте он автоматически заменится на имя игрока, и позволит открыть профиль (напр: "оповещение на 76561198121100397" заменится на "оповещение на **playername**").

</details>

## 🪝 Hooks

### Перехват действий

Вызывается перед отоборажением уведомления о проверке, если вернуть не null - табличка показана не будет
```csharp
object RustApp_CanIgnoreCheck(BasePlayer player)
```

Вызывается перед отправкой жалобы, если вернуть не null - жалоба отправлена не будет
```csharp
object RustApp_CanIgnoreReport(string target_steam_id, string initiator_steam_id)
```

Вызывается перед проверкой на блокировки, если вернуть не null - баны проверены не будут
```csharp
object RustApp_CanIgnoreBan(string steam_id)
```

Вызывается перед открытием UI жалоб, если вернуть не null - интерфейс открыт не будет
```csharp
object RustApp_CanOpenReportUI(BasePlayer player)
```

### События

Табличка о вызове на проверку показана
```csharp
RustApp_OnCheckNoticeShowed(BasePlayer player)
```

Табличка о вызове на проверку скрыта
```csharp
RustApp_OnCheckNoticeHidden(BasePlayer player)
```

#### События ниже - доступны только начиная с определённого тарифа

`Starter` Игрок был заблокирован. Третий аргумент - список игроков которые жаловались на этого игрока
```csharp
RustApp_OnPaidAnnounceBan(BasePlayer player, string steam_id, List<string> initiators)
```

`Starter` Игрок был проверен, и нарушений не обнаружено. Третий аргумент - список игроков которые жаловались на этого игрока
```csharp
RustApp_OnPaidAnnounceClean(BasePlayer player, string steam_id, List<string> initiators)
```
