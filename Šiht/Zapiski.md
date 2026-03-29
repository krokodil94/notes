1. General Concepts

Standard pokriva:
  - Device management sistem - naš DM agent
  - Data Flow management sistem - naš DFM agent
  - Aler management - to je implementirano znotraj DFM Agenta - ALARM AGENT

2. Komunikacija med sistemi

  2.1 

    Zahteva po uporabi TLS (X.509) digitalnega certifikata s strani Management uinta/Edge unita da lahko komunicira z IoT platformo

    MQTTS in SFTP že uporabljata username in geslo, pri HTTPS pa je potrebno dodati JWT. 

    Acess control List je trenutno implementirana v obliki config.json datoteke, kjer se lahko konfigurira vsaka naprava posebej. Config.json se lahko upravlja preko MQTTS



2.1.1 JWT Token 

 Ne razumem čist, bo treba še mal bolj raziskat

 2.2 Summary of the Specification

 Alert management - Alarm Management- OK, nekaj podobnega ze implementiranega
 Alert Management - Fault Management -  Tudi ze nekaj podobnega implementiranega - javlja za naprave ki manjkajo


 Data Flow Management - Submission measurement - To je implementirano kot REQUEST_FOR_DATA, vendar zaenkrat še ni moznosti definirat
                      - Bulk transmission - to je pa ze identično trenutni implementaciji


2.3 Protokoli

Zahteva MQTT 5.0 -> trenutno uporabljamo 3.1. Za en del more grega rebuildat historian dll.

TLS -> enako treba v DLL preveriti. V DM agent delu mislim da imamo to urejeno
Potrebno je urediti/dodati še to, da se lahko QoS spreminja - configurable parameter

3. Alarm Management and Data Flow

  1.) Alarms - Nikjer niso zdefinirani tipi alarmov, in tipi sporočil ki jih pošlje alarm. Nekaj je implementirano v Alarm agentu, v kolikor nam uspe, bi bilo verjetno najboljše implementirati čimbolj podobno.

    - Pre-alert (Events) - tega trenutno nimamo čist nič implementiranga
    - Alert - To je pa implementirano, sam nimamo alarm levela, in intensitya - kar pa tut v standardu ni dobr zdefinirano.