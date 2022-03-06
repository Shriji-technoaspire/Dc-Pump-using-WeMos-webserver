#include <ESP8266WiFi.h>
#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "Pump Controller";
const char* password = "12345678";

ESP8266WebServer server(80);

const int pump = 8;
static const String page PROGMEM = "<h1>Water Pump Controller</h1><p><a href=\"PumpOn\"><button>ON</button></a>&nbsp;<a href=\"PumpOff\"><button>OFF</button></a></p>";
 
void setup(void) {
  
  pinMode(pump, OUTPUT);
  digitalWrite(pump, 0);
  Serial.begin(115200);
 
  WiFi.softAP(ssid, password);
  Serial.println("");

  Serial.println(ssid);
  Serial.print("WiFi Server started at IP address: ");
  Serial.println(WiFi.softAPIP());


  server.on("/", [](){
    server.send(200, "text/html", page);
  });
  
  server.on("/PumpOn", [](){
    server.send(200, "text/html", page);
    digitalWrite(pump, HIGH);
    delay(1000);
  });
  
  server.on("/PumpOff", [](){
    server.send(200, "text/html", page);
    digitalWrite(pump, LOW);
    delay(1000);
  });

  server.begin();
  Serial.println("HTTP server started");
}

void loop(void) {
  server.handleClient();
}
