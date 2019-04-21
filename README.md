# Уведомление об авторизации на linux системах через telegram
Для уведомления через телеграм об авторизации на linux системах необходимо создать файл [/usr/bin/login-notify](login-notify), сделать его исполняемым.  
Исправить переменные **token** и **chat** на ваши.  
**token** - это токен вашего бота, как создать бота  
**chat** - это ID получателя  
Уведомления будут приходить от сервисов SSH, su, login, sudo и др. использующих PAM авторизацию.  

## Использование  
### Debian
Поместите строку 
*session optional pam_exec.so /usr/bin/login-notify*
в конец файл */etc/pam.d/common-session*
```
echo "session optional pam_exec.so /usr/bin/login-notify" >> /etc/pam.d/common-session
```

Для корректной работы необходим установленный пакет *dnsutils* (содержит dig).  

### Как узнать токен вашего бота
Можно [создать бота](http://bernaerts.dyndns.org/linux/75-debian/351-debian-send-telegram-notification#create_your_telegram_bot)
```
1.1. Create your Telegram Bot
Telegram allows you to easily create your own Bot with the help of @BotFather.

This page explain very clearly what you can expect from your Telegram Bot and how to create it.

To make it short, a Bot is a type of Telegram account that doesn't need to be associated to a phone number. It's an application account associated to your personnal account.

Once you have created your Bot, you get your API key. This key looks like 123456789:AABBCCDD_abcdefghijklmnopqrstuvwxyz.

As Telegram APIs are using plain httpsURL with POST data, this API key is needed to identify the Bot when you send messages, photos and documents straight from any web client.

All parameters are explained in Telegram API page.

Your Bot will be able to send messages either to :

your personnal account
any channel it belongs to
But to send any message, your Bot will need to use either your user ID or a Channel ID. It can not address an account simply using its name.

Here is the way to get these IDs.
```
Для того чтобы получать сообщения от бота - пользователь должен послать этому боту любое сообщение.

 ### [как узнать ID получателя](http://bernaerts.dyndns.org/linux/75-debian/351-debian-send-telegram-notification#h1-2-get-your-user-id)  
ID это номер, узнать его можно следующим образом.
```
1.2. Get your User ID
To get your user ID, you just need to :

send a message to your Bot from your Telegram client
call the following URL from any web browser
 URL	 https://api.telegram.org/bot123456789:AABBCCDD_abcdefghijklmnopqrstuvwxyz/getUpdates
 Answer	 {"ok":true,"result":[{"update_id":563273027,"message":{"message_id":505, "from":"id":11223344, "first_name":"YourFirstName", "last_name":"YourLastName", "username":"YourUserName"},
"chat":{"id":11223344, "first_name":"YourFirstName", "last_name":"YourLastName", "username":"YourUserName", "type":"private"}, "date":1483150094, "text":"Hello bot !"}}]}
 

You can see here that your user ID is 11223344.

This is the client ID that Telegram Bot should use to send me a message.
```

#### Ссылки:
[Debian - Send your Server Notifications thru Telegram](http://bernaerts.dyndns.org/linux/75-debian/351-debian-send-telegram-notification)  
[Login notifications, pam_exec scripting](https://blog.stalkr.net/2010/11/login-notifications-pamexec-scripting.html)  
