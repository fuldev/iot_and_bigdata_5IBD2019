# iot_and_bigdata_5IBD2019
Dans ce projet on réccupère la valeur de l'humidité de la plante avec une interface web et ESP8266 et puis on agit sur un servo moteur qui simule l'ouverture et la fermeture du robinet pour arroser ou arrêter l'arosage de la plante.
Dans ce wiki nous expliquons les différents étapes de notre projet : 
https://github.com/fuldev/iot_and_bigdata_5IBD2019/


# Les dependances de notre projet


server.h    : à installer dans Gérer les les bibliothèques Arduino IDE 

ESP8266WIFI   : à installer aussi dans Gérer les les bibliothèques Arduino IDE 

LOLIN(WEMOS) D1 R2 & mimi  : les types de carte qu'il faut spécifier dans Arduino IDE


# Explication du code 

● d'abord on définit DHT11 comme type de capteur : 
>		
	○ #define DHTTYPE DHT11 
  

● puis  on définit les paramètre de notre wifi: 
>		
	○ const char* ssid = "WX3"; 
	○ const char* password = "";
	
● ensuite on définit le pin et le type  : 
>		
	○ const int DHTPin = D4;
	○ DHT dht(DHTPin, DHTTYPE);

● On définit le contenu de nore fonction setup de cette manière  : 
>		
	○  void setup() {
 
        ○  myservo.attach(D5);  // on attache notre servo moteur au pin D5

        ○  Serial.begin(115200);   // le begin faut le specifier dans le moniteur 
  
        ○  delay(10);

        ○  dht.begin();
  
        ○  // là on se connecte au wifi
 
        ○  Serial.println();
  
        ○  Serial.print("Connecting to ");
  
        ○  Serial.println(ssid);  
  
        ○  WiFi.begin(ssid, password);  // on indique les paramètres de wifi déjà indiqués
  
        ○  while (WiFi.status() != WL_CONNECTED) {
  
        ○  delay(500);
      
        ○  Serial.print(".");
 
        ○  }
	
        ○ Serial.println("");
  
        ○  Serial.println("WiFi connected");
  
        ○  // on lance notre web serveur
 
        ○  server.begin();
  
        ○ Serial.println("Web server running. Waiting for the ESP IP...");
  
        ○ delay(10000);
  
        ○ //  on affiche notre ESP IP adresse
  
        ○ Serial.println(WiFi.localIP());
        ○ }


● on lit les valeurs capté par sensor de cette manière :
>		
	○  float h = dht.readHumidity();  // on lit l'humidité
  
     ○  float t = dht.readTemperature();   // on lit la température  avec l'unité Celsius
	
	○  float f = dht.readTemperature(true);   // on lit la température  avec l'unité Fahrenheit (isFahrenheit = true)

  // Computes temperature values in Celsius + Fahrenheit and Humidity
                    
                         
              
                           
                
              

● on calcule la tempértaure valeurs en Celsius + Fahrenheit and Humidity  :
>		
	○  hic = dht.computeHeatIndex(t, h, false); 
  
        ○  dtostrf(hic, 6, 2, celsiusTemp);
	
	○  float hif = dht.computeHeatIndex(f, h);
	
	○  dtostrf(hif, 6, 2, fahrenheitTemp); 
	
	○  dtostrf(h, 6, 2, humidityTemp);  
	          
	
● et finalement on affiche nos valeurs dans le navigateur web avec le code html suivant :
>		
	○  client.println("<!DOCTYPE HTML>");
  
        ○  client.println("<html>");
	
	○  client.println("<head></head> <meta http-equiv='Content-Type' content='text/html'; charset='UTF-8' /> <style> body {                 ○ background-color: #fffff; font-family: Arial, Helvetica, Sans-Serif; Color: #000088; }</style> <body><h1>ESP8266 - Plants             ○ System</h1><h3>Temperature in Celsius: ");
	
	○  client.println(celsiusTemp);
	
	○   client.println("*C</h3>"); 	
	
	○   client.println("<h3>Temperature in Fahrenheitt: ");
	
	○   client.println(fahrenheitTemp);
	
	○   client.println("*F</h3>");
	
	○   client.println("<h3>Humidity: ");
	
	○   client.println(humidityTemp);
	
	○   client.println("%</h3><h3>");
	
	
