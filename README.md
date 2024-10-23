## POS сервер  

Промежуточное  ПО для подключения принтеров  и торгового оборудования к учетным  программам, работающим  в онлайн режиме (через браузер) 
и, соответственно не  имеющим  возможности напрямую подключаться  к  торговому  оборудованию. 
Разработано для проекта <https://github.com/leon-mbs/zstore> но может использоваться  и с другми системами.  
Сервер  реализует  API, к которому учетная програма  обращается  с браузера с помощью javascript запроса как  к  обычному  веб серверу. 
Для обмена  данными используется  формат json.

Готовой реализацией является  режим  принт-сервера для работы  с  чековыми  принтерами  и принтерами этикеток, подключаемыми  по  USB. 
Остальные  режимы реализуются  кастомно  в  зависимлсти от типа  оборудования  

Адрес сервера задается  в  конфигурационных файлах.  По умолчанию http://127.0.0.1:8080  
Проверка  сервера с  браузера  http://127.0.0.1:8080/check  

### Работа с  принтером  (режим принт сервера)
Проверка  принтера с  браузера  http://127.0.0.1:8080/testprint  
На принтере должна распечататься тестовая  строка.  
Имя принтера (как оно задано в списке принтеро виндовс) прописывается  в  appsettings.json

POST /print  - точка  входа для печати.  Учетная програма должна  отправить массив  байтов типа  [34,456,54]  которые  принт сервер 
перенаправит на принтер.  Если все  в  порядке  функция возвращает пустую строку иначе  сообщение об ошибке  


### Работа с весами
 POST /weight   
 content-type: application/json   
 {  
    "posid":1   //id pos терминала  или кассового места   
 } 
 
 ответ  
 {  
    "success":true,  
    "weight":1.6    //вес     
 } 
 или  
 {  
    "success":false,  
    "error":"invalid data"    //текст ошибки     
 } 


 ### Банковский  терминал  
 POST /bankpay   
 content-type: application/json   
 {  
    "amount":1.5   //сумма
 } 
 
 ответ  
 {  
    "success":true,  
    "tranid":"ID345654"    //номер банковской  транзакции
 }    
  или  
 {  
    "success":false,  
    "error":"invalid data"    //текст ошибки     
 } 

     




