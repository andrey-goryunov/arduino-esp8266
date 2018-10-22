//#define BLYNK_PRINT Serial
#define BLYNK_MAX_SENDBYTES 1024
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <TimeLib.h>
#include <WidgetRTC.h>
#include <math.h>

#define TERMIST_B 4300
#define VIN 3.3
#define PIR D1                  // инфрокрасный датчик, PIR Sensor
#define LED D4                  // светодиод (инвертирован)
#define RELAY D8                // D8 = gpio 15 реле
#define BUZZER D7               // D7 = gpio 13 пищалка

#define BLYNK_GREEN     "#23C48E"
#define BLYNK_BLUE      "#04C0F8"
#define BLYNK_YELLOW    "#ED9D00"
#define BLYNK_RED       "#D3435C"
#define BLYNK_DARK_BLUE "#5F7CD8"
#define BLYNK_WHITE     "#FFFFFF"

char Mail[] = "gryn87@gmail.com";          // e-mail, куда будет все отправляться
String Subject = "Subject: Security ESP "; // тема сообщения на e-mail

char auth[] = "2c824734932b46e4a1fd47f1d17e9da9";
char ssid[] = "G";
char pass[] = "4ebyrashka";

WidgetTerminal terminal(V8);    // регистрируем виджет-терминал
WidgetRTC rtc;                  // инициализируем виджет часов реального времени
BlynkTimer timer;               // инициализируем таймер

int timerSpeak_ID;              // инициализируем переменную для хранения ID таймера пищалки
int timerPIRSensor_ID;          // инициализируем переменную для хранения ID таймера датчика движения

bool isFirstConnect = true;     // Переменная для хранения состояния первый раз ли установленна связь
bool pirState = false;          // Инициализируем пременную для хранения состояния срабатываия сигнализации датчика движения

bool flagProtection = false;    // Пеменная для хранения состояния сигнализации (пригодится для усиления безопасности)
bool intruderState = LOW;       // Переменна которая хранит сработку сигнализации
int securityStateX = 0;         // Номер состояния сигнализации

WiFiClientSecure clientSecure;  // это нужно для функций GET запроса по HTTPS
WiFiClient client;              // HTTP
const int httpPort = 8023;      // HTTP порт 
const int httpsPort = 443;      // HTTPS порт 
const char* httpHost = "192.168.1.41";
const char* httpsHost = "golgo.ru";


BLYNK_WRITE(V9)                          // TEST DEV
{
  if (param.asInt()) {
    
    Blynk.setProperty(V9, "color", BLYNK_RED);     // включаем
    terminal.println(F("V9 ON"));
    terminal.flush();
    
  } else {
    
    Blynk.setProperty(V9, "color", BLYNK_WHITE); // выключаем
    terminal.println(F("V9 OFF"));
    terminal.flush();
  }
}


BLYNK_WRITE(V15)                         // Recording button
{
  if (param.asInt()) {
    
    GetHTTPSRequest("recording.sh");     // включаем
    terminal.println(F("recording..."));
    terminal.flush();
    
  } else {
    
    GetHTTPSRequest("stop-recording.sh"); // выключаем
    terminal.println(F("stop-recording ..."));
    terminal.flush();
  }
}


BLYNK_WRITE(V12)                         // Кнопка Screenshoot send
{
  if (param.asInt()) {
    GetHTTPSRequest("screenshoot.sh"); 
    terminal.println(F("send screenshoot ..."));
    terminal.flush();
 
  } else {
  }
}


BLYNK_WRITE(V17)                         // Write received string to local terminal from Wemos 4.0
{
  String pinData = param.asStr();
  terminal.println(pinData);             
  terminal.flush();
}


BLYNK_WRITE(V16)                         // Start & Stop video stream from video0 webcam on Sirius
{
  int i=param.asInt();
  if (i==1) {
    GetHTTPSRequest("start-stream.sh");   // GET to golgo
  }
  else {
    GetHTTPSRequest("stop-stream.sh");    // GET to golgo
   }
}


BLYNK_WRITE(V4)                          // Кнопка info - посылает в виджет-терминал сообщение
{
  String currentTime = String(hour()) + ":" + minute() + ":" + second();
  String currentDate = String(day()) + "/" + month() + "/" + year();

  if (param.asInt()) {
    terminal.print(currentDate + (" ") + currentTime + (" current ip: "));
    terminal.println(WiFi.localIP());
    terminal.println(F("Wemos 3.4 with BLYNK v" BLYNK_VERSION ": Device online"));
    terminal.flush();
  }

  else {
  }
}


BLYNK_WRITE(V5)                          // Music Player widget - VLC
{
  String action = param.asStr();

  if (action == "play") {
    GetHTTPRequest("play");
    terminal.println(F("Play"));
    terminal.flush();
  }
  
  if (action == "stop") {
    GetHTTPRequest("stop");
    terminal.println(F("Playback stopped"));
    terminal.flush();
  }
  
  if (action == "next") {
    GetHTTPRequest("next");
    terminal.println(F("Next >>"));
    terminal.flush();
  }
  
  if (action == "prev") {
    GetHTTPRequest("prev");
    terminal.println(F("Previous <<"));
    terminal.flush();
  }

  Blynk.setProperty(V5, "label", action);
  //Serial.print(action);
  //Serial.println();
}


BLYNK_WRITE(V3)                          // ползунок громкости для vlc.py
{
  int pinValue = param.asInt();          // assigning incoming value from pin V3 to a variable
  // You can also use:
  String i = param.asStr();
  // double d = param.asDouble();
  
  GetHTTPRequest(i);
  terminal.print(F("audio volume: "));
  terminal.println(i);
  terminal.flush();
}


BLYNK_WRITE(V6)                          // Включает и выключает компьютер
{
  String currentTime = String(hour()) + ":" + minute() + ":" + second();
  String currentDate = String(day()) + "/" + month() + "/" + year();
  
  if (param.asInt()) {
    
    GetHTTPSRequest("wake-home.sh");     // включаем
    terminal.print(currentDate + (" ") + currentTime + (": "));
    terminal.println(F("home wake up"));
    terminal.flush();
    
  } else {
    
    GetHTTPSRequest("poweroff-home.sh"); // выключаем
    terminal.print(currentDate + (" ") + currentTime + (": "));
    terminal.println(F("poweroff home"));
    terminal.flush();
  }
}


void GetHTTPRequest(String url)          // Функуция отправялет GET запрос к home
{
  if (client.connect(httpHost, httpPort)) {
    client.println("GET /?key=" + url + " HTTP/1.1");
    client.println("Host: 192.168.1.47");
    client.println("Content-Type: application/x-www-form-urlencoded");
    client.println("User-Agent: wemos 3.3");
    client.println("Connection: close");
    client.println();
    client.stop();
    delay(1);
  }
}


void GetHTTPSRequest(String url)         // Функуция отправялет GET запрос к golgo.ru
{
  if (clientSecure.connect(httpsHost, httpsPort)) {
    clientSecure.println("GET /uxahMah5quoo4iew/" + url + " HTTP/1.1");
    clientSecure.println("Host: golgo.ru");
    clientSecure.println("Content-Type: application/x-www-form-urlencoded");
    clientSecure.println("User-Agent: wemos 3.3");
    clientSecure.println("Connection: close");
    clientSecure.println();
    clientSecure.stop();
    delay(1);
  }
}


BLYNK_WRITE(V2)                          // Считываем состояние кнопки "Активировать датчик движения" и сохраняем значение в flagProtection
{
  flagProtection = param.asInt();        // Читаем состояние кнопки

  if (flagProtection) {                  // если флаг поднят
    timer.enable(timerPIRSensor_ID);     // Включить таймер для функции readPIRSensor
  }
  else {
    timer.disable(timerPIRSensor_ID);    // Отключить таймер для функции readPIRSensor
    timer.setTimeout(50, readPIRSensor); // Дергаем функцию Датчика Движения один раз с задержкой 50 Милесукунд
  }
}


BLYNK_CONNECTED()                        // Если установили связь первый раз, то синхонезируем все виджеты
{
  if (isFirstConnect) {
    Blynk.syncAll(); // синхонезируем все виджеты

    // Составляем строки с временем и датой и добовляем их к сообщению
    //String currentTime = String(hour()) + ":" + minute() + ":" + second();
    //String currentDate = String(day()) + "/" + month() + "/" + year() + " ";
    //String Notif = "Оборудование Запущено  " + currentDate + " " + currentTime;
    
    //Blynk.notify(Notif);

    // Отправка на почту
    //Blynk.email(Mail, Subject, Notif); // хотя отправлять другим способом (строкой ниже)
    //Blynk.email("sibeng24@gmail.com", "Subject: Security ESP ", "Оборудование Запущено"); // стандартная отправка на мыло
    isFirstConnect = false;

  }
}


BLYNK_READ(V14)                          // TERMIST_B
{
  float voltage = analogRead(A0) * VIN / 1024.0;
  float r1 = voltage / (VIN - voltage);
  float t = 1. / ( 1. / (TERMIST_B) * log(r1) + 1. / (25. + 273.) ) - 273;
  Blynk.virtualWrite(V14, t);            //sending to Blynk
}


void readPIRSensor()                     // функция для считывания показаний датчика движения
{
  static int pir = LOW; // объявляем переменную для хранения информации о состоянии цыфрового входа PIR
  
  /* 
   *  Ключевое слово static используется для создания переменной,
   *  которая видна только одной функции. Однако в отличие от локальных переменных,
   *  которые создаются и уничтожаются при каждом вызове функции,
   *  статические переменные остаются после вызова функции, сохраняя свои значения между её вызовами.
  */

  if (flagProtection == true && pirState == LOW)   // Если сигнализация включена
  {
    pir  = digitalRead(PIR);                       // читаем значение с цифрового входа
  }
  
  // мы не интересуемся состоянием датчика, пока охрана не включена

  if (flagProtection == true && pir == HIGH && pirState == LOW) // Если сигнализация Включена (ON) и Датчик Движения сработал
  { 
    pirState = HIGH;                               // Этот флаг можно сбросить только отключив сигнализацию
    digitalWrite(LED, !pirState);                  // включаем светодиод на плате
  }

  if (flagProtection == false && pirState == HIGH) // Если сигнализация Выключена (OFF) и была сработка
  { 
    pirState = LOW;                                // Сбрасываем флаг
    digitalWrite(LED, !pirState);                  // выключаем светодиод
  }
}


void refreshState()                      // Если замечено движение, перезапускает наблюдение, используя для этого АЖ ДВЕ ФУНКЦИИ
{
    flagProtection = false;
    intruderState == HIGH;
    GetHTTPSRequest("stop-stream.sh");
    timer.setTimer(2000, reactiveSecurity, 1);  // это наверно не хорошо
}


void reactiveSecurity()                  // как объеденить это в одну функцию?
{
    securityStateX = 0;  
    flagProtection = true;
    pirState == true;
}


void securityState()                     // Определяем состояние Сигнализации и производим соответствущие действия
{

  // Состояние 1 
  // "Если охрана Включена" и "Сработал датчик" и "Не в Состоянии 1"
  // Код выполнится один раз
  if (flagProtection == true && pirState == true && securityStateX != 1)
  {
    terminal.println(F("system callback: securityStateX change to 1"));
    terminal.flush();
    securityStateX = 1;                           // Номер состояния сигнализации 1
    intruderState = HIGH;                         // СИГНАЛИЗАЦИЯ СРАБОТАЛА
    timer.setTimer(1000, messeg, 3);              // вызываем функкцию messeg 3 раза, с интервалом в 1 секунду
    //digitalWrite(RELAY, intruderState);         // Срабатывает реле
    timer.setTimer(200, sendSetting, 4);          // вызываем функкцию sendSetting 4 раза, с интервалом в 0,2 секунд
    timer.enable(timerSpeak_ID);                  // Включить таймер для функции Speak Пищалка
    GetHTTPSRequest("screenshoot.sh");            // отправляем скриншот
    delay(10);
    timer.setTimer(12000, refreshState, 1);       // через это время сига отключится и включится вновь (что бы записывать только движения)
    
  }

  // Состояние 2 
  // "Если охрана Включена" и "Датчик Не Сработал" и "Не в Состоянии 2"
  // Код выполнится один раз
  else if (flagProtection == true && pirState == false && securityStateX != 2)
  {
    securityStateX = 2;                   // Номер состояния сигнализации 2
    timer.setTimer(1000, messeg, 3);      // вызываем функкцию messeg 3 раза, с интервалом в 1 секунду
    timer.setTimer(200, sendSetting, 4);  // вызываем функкцию sendSetting 4 раза, с интервалом в 0,2 секунд
  }

  // Состояние 3 
  // "Если охрана Выключена" и "Сигнализация Сработала" и "Не в Состоянии 3"
  // Код выполнится один раз
  else if (flagProtection == false && intruderState == HIGH && securityStateX != 3)
  {
    securityStateX = 3;                   // Номер состояния сигнализации 3
    intruderState = LOW;                  // Обнуляем флаг сработки Сигнализации
    timer.disable(timerSpeak_ID);         // Выключаем пищалку
    GetHTTPSRequest("stop-stream.sh");    // завершаем стрим с камеры
    timer.setTimer(1000, messeg, 3);      // вызываем функкцию messeg 3 раза, с интервалом в 1 секунду
    timer.setTimer(200, sendSetting, 4);  // вызываем функкцию sendSetting 4 раза, с интервалом в 0,2 секунд  
    terminal.println(F("system callback: securityStateX change to 3"));
    terminal.flush();
  }

  // Состояние 4 
  // "Если охрана Выключена" и "Сигнализация Не Сработала" и "Не в Состоянии 4"
  // Код выполнится один раз
  else if (flagProtection == false && intruderState == LOW && securityStateX != 4)
  {
    if (securityStateX != 3)               // если предидущее состояние не равно 3 то
    {
      securityStateX = 4;                  // Номер состояния сигнализации 4
      timer.setTimer(1000, messeg, 3);     // вызываем функкцию messeg 3 раза, с интервалом в 1 секунду
      timer.setTimer(200, sendSetting, 4); // вызываем функкцию sendSetting 4 раза, с интервалом в 0,2 секунд
    }
  }
}


void messeg()                            // функция для отправки сообщений, в зависимости от статуса сигнализации (securityState)
{
  String Notif; // Переменная для хранения сообщения
  String currentTime = String(hour()) + ":" + minute() + ":" + second();  // Опрашиваем RTC и составляем строки для отправки
  String currentDate = String(day()) + "/" + month() + "/" + year() + " ";

  // в зависимости от состояния сигнализации выбираем нужный текст
  // и прибавляем значение даты и времени
  switch (securityStateX) {
    case 1:
      Notif = "Чужой на ОБЪЕКТЕ  " + currentDate + " " + currentTime;
      break;
    case 2:
      Notif = "Охраняется  " + currentDate + " " + currentTime;
      break;
    case 3:
      Notif = "Снято с охраны, после обноружения НАРУШИТЕЛЯ  " + currentDate + " " + currentTime;
      break;
    case 4:
      Notif = "Не наблюдается  " + currentDate + " " + currentTime;
      break;

      //default:
      // код для выполнения
  }

  static int i = 1; // переменная и конструкция из if else нужна для
  // последовательной отправки с задержкой

  // отправляем сообщения
  // здесь можно просто закоментировать не нужный нам способ связи

  if (i == 3) {
    //Blynk.notify(Notif);
    i = 1;
  }

  else if (i == 2) {
    //Blynk.email(Mail, Subject, Notif);
    i++;
  }

  else if (i == 1) {
    //Blynk.tweet(Notif);
    i++;
  }

}


void Setting (String color, String Text) // Меняем цвета и выводим сообщение, зависит от (securityState)
{
  
  static int i = 1;                           // переменная и конструкция из if else нужна для последовательной отправки с задержкой

  if (i == 4) {
    //led1.setColor(color);                   // Меняем цвет LED V1
    i = 1;
  }

  else if (i == 3) {
    Blynk.setProperty(V10, "color", color);   // Меняем цвет виджета V10
    i++;
  }
  else if (i == 2) {
    Blynk.setProperty(V2, "color", color);    // Меняем цвет виджета V2
    i++;
  }
  else if (i == 1) {
    Blynk.virtualWrite(V10, Text);            // Выводим сообщение в Value Display
    i++;
  }

}


void sendSetting()                       // Совершаем действия в зависимости от статуса сигнализации (securityState).
{

  String Notif; // Переменная для хранения сообщения
  String color; // Переменная для хранения цвета

  // тут выбераем настройки в зависимости от состояния системы
  switch (securityStateX) {
    case 1:
      Notif = "Обнаружено движение";
      color = BLYNK_RED;
      break;
    case 2:
      Notif = "Охраняется";
      color = BLYNK_YELLOW;
      break;
    case 3:
      Notif = "Снято с охраны. Был нарушитель";
      color = BLYNK_YELLOW;
      break;
    case 4:
      Notif = "Не наблюдается";
      color = BLYNK_GREEN;
      break;
  }
  // вызываем функцию Setting и подставляем в нее данные
  Setting(color, Notif); // Настраиваем виджеты (меняем цвета выводим сообщение)
}


void Speak()                             // Функция для Зуммера Пищалки (Кричалки)
{
  // Задаем частоту и длительность для пищалки
  tone(BUZZER, 3500, 50);
} // Speak


void reconnectBlynk()                    // функция которая проверяет соединение
{
  if (!Blynk.connected()) { //если соединения нет то
    if (Blynk.connect()) {  // конектимся
      BLYNK_LOG("Reconnected");    // выводим в лог

    } else {
      BLYNK_LOG("Not reconnected"); // выводим в лог
    }
  }
}


void setup()                             // настройки
{
  // Debug console
  //Serial.begin(19200);
  //Serial.println(" ");
  //Serial.println("Launch");

  // Настраиваем входы и выходы
  pinMode (LED, OUTPUT);
  digitalWrite(LED, HIGH);
  pinMode (RELAY, OUTPUT);
  pinMode (PIR, INPUT);
  pinMode (BUZZER, OUTPUT);

  delay(1000);

  for (int i = 0; i <= 3; i++) {
    tone(BUZZER, 300, 50);
    delay(80);
  }

  Blynk.begin(auth, ssid, pass, IPAddress(192, 168, 1, 66), 8442);
  Blynk.disconnect(); //разорвать соединение
  Blynk.connect();    // а потом пробуем уже конектиться

  // Настраиваем таймеры
  timerPIRSensor_ID = timer.setInterval(1250L, readPIRSensor); // Дергаем функцию датчика движения раз в пол секунды
  timerSpeak_ID = timer.setInterval(500L, Speak);              // Дергаем функцию
  timer.disable(timerPIRSensor_ID);                            // отключаем таймер Датчика Движения
  timer.disable(timerSpeak_ID);                                // отключаем таймер Пищалки
  timer.setInterval(3000L, securityState);                     // Дергаем функцию Статуса охраны раз в секунду
  timer.setInterval(160000L, reconnectBlynk);                  // проверяем каждые 30 секунд, если все еще подключен к серверу

  rtc.begin(); // запускаем виджет часов реального времени

  // Настраиваем виджеты
  // led1.on();

  // Меняем название виджета V10 (Value Display)(понимает только английский)
  Blynk.setProperty(V10, "label", "Security status"); // Настраиваем название Виджета
  
  //Serial.println("Ready");
  //Serial.print("IP address: ");
  //Serial.println(WiFi.localIP());
    terminal.println(F("Wemos 3.3 with BLYNK v" BLYNK_VERSION ": Device started"));
    terminal.flush();
    
// ----------    
  if (Blynk.connected()) {         // Если установили связь, то два раза Пищалкой Пискнем
    for (int i = 0; i <= 2; i++)
    { tone(BUZZER, 200, 50);
      delay(100);
    }
  }
  else {
    for (int i = 0; i <= 10; i++)  // Если не установили связь, то 10 раза Пищалкой Пискнем
    { tone(BUZZER, 100, 50);
      delay(80);
    }
  }
// ----------
  
}


void loop()                              // запуск программы
{
  if (Blynk.connected()) {
    Blynk.run(); // Запускаем Блинк
  }
  timer.run();   // Запускаем таймер
}
