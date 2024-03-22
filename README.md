## Плагин RustApp
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

   <br>Для отправки репортов в RustApp можно использовать и свою систему жалоб, но для этого необходимо интегрировать свой плагин с плагином RustApp.
   
   ```csharp
   plugins.Find("RustApp")?.Call("RA_ReportSend", initiatorId, targetID, reason, <optional> message)
   ```
   `senderId` - String SteamID64 того, кто жалуется\
   `targetId` - String SteamID64 того, на кого жалуются\
   `reason` - причина жалобы (читы/макросы и т.д)\
   `message` - комментарий к репорту (можно не передавать, если Ваш плагин не поддерживает комментарии к жалобам)

   ⚠️ Не забудьте из конфигурации `RustApp.json` убрать все команды, чтобы наше UI нельзя было открыть!

</details>

## 🪝 Hooks

Табличка о вызове на проверку показана
```csharp
RustApp_OnCheckNoticeShowed(BasePlayer player)
```

Табличка о вызове на проверку скрыта
```csharp
RustApp_OnCheckNoticeHidden(BasePlayer player)
```
