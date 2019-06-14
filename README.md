# iot_and_bigdata_5IBD2019
Dans ce projet on réccupère la valeur de l'humidité de la plante avec une interface web et ESP8266 et puis on agit sur un servo moteur qui simule l'ouverture et la fermeture du robinet pour arroser ou arrêter l'arosage de la plante.
Dans ce wiki nous expliquons les différents étapes de notre projet : 
https://github.com/fuldev/iot_and_bigdata_5IBD2019/


# Les dependances de notre projet

ESP8266 Arduino:

https://github.com/esp8266/Arduino#installing-with-boards-manager

server.h    : à installer dans Gérer les les bibliothèques Arduino IDE 

ESP8266WIFI   : à installer aussi dans Gérer les les bibliothèques Arduino IDE 

LOLIN(WEMOS) D1 R2 & mimi  : les types de carte qu'il faut spécifier dans Arduino IDE


# Explication du code 

● d'abord on définit DHT11 comme type de capteur : 
>		
	○ #define DHTTYPE DHT11 
  







