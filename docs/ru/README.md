![Logo](admin/hilink.png)   
 
# ioBroker.hilink   
=================

## Описание

Драйвер для USB модемов Huawei с прошивками Hilink.   

Проверенно на модемах:    
E3372h-153_Update_22.323.01.00.143_M_AT_05.10    
E3372s Update_22.286.53.01.161_S_ADB_TLN_03    


Прошивки и другую информацию можно найти тут - http://4pda.ru/forum/index.php?showtopic=582284&   


Совместимость E3372 (МТС 827F/829F, МегаФон M150-2, Билайн E3372/E3370, TELE2 E3372р-153

- подключение, отключение от сети и перезагрузка модема
- чтение входящих и исходящих сообщений.
- отправка сообщений.
- отправка ussd запросов.
- получение основных параметров модема, информация о трафике.


```javascript

//  Подключение 'conect', отключение 'desconect' от сети и перезагрузка модема 'reboot'

sendTo("hilink.0",'control','reboot',function (response){
    log(JSON.stringify( response, null, 2 ));
});

sendTo("hilink.0",'control','conect');

// отправка сообщения
sendTo("hilink.0",'send',{
    phone:  '+7123456789', // номер телефона
    message:  'Проверка работы' // текст сообщение
    },function (response){
    log(JSON.stringify( response, null, 2 ));
});

sendTo("hilink.0",'send',{phone:'+7123456789',message:  'Проверка работы'});


// чтение сообщений 
sendTo("hilink.0",'read','inbox',function (response){
     log(JSON.stringify( response, null, 2 ));
});

/*
'inbox' входящих, 
'outbox' исходящих, 
'new' чтение входящих только новые сообщение 
*/


//отправка ussd запроса
sendTo("hilink.0",'ussd','*100#',function (response){
     log(JSON.stringify( response, null, 2 ));
});

// удаление одного сообщения с индексом '40002'
sendTo("hilink.0",'delete','40002',function (response){
     log(JSON.stringify( response, null, 2 ));
});

// очистка всех 'outbox' исходящих, 'inbox' входящих сообщений
sendTo("hilink.0",'clear','outbox',function (response){
     log(JSON.stringify( response, null, 2 ));
});

```

## Changelog

#### 0.2.2
* (bondrogeen) add json last sms

#### 0.0.5
* (bondrogeen) fix last sms

#### 0.0.4
* (bondrogeen) fix

#### 0.0.3
* (bondrogeen) add 3372h

#### 0.0.1
* (bondrogeen) initial release
