# ESP-task
#define LED_RED 26 /*the pin that the positive leg of the LED will be connected to*/

void setup() {
  // put your setup code here, to run once:
  pinMode(LED_RED,OUTPUT);/*configuring the pin as an output pin*/
  Serial.begin(115200);/*idk???*/
  Serial.println("Hello, ESP32!"); /*prints a message on the console to inform that the 
  processor got to the end of the setup function*/
}

void loop() {
  digitalWrite(LED_RED,HIGH);/*turns ON my LED*/
  Serial.println("ON");/*helps me detect errors in case of any failure in my code/hardware*/
  delay(1000);/*keeps the LED ON for a set period of time*/
  digitalWrite(LED_RED,LOW);/*turns OFF my LED*/
  Serial.println("OFF");/*helps me detect errors in case of any failure in my code/hardware*/
delay(1000);/*keeps the LED OFF for a set period of time*/
}/*first code*/












#define LED_RED 26 /*the pin that the positive leg of the LED will be connected to*/
#define pot     36
/*where are the other definitions such as output and input, low/high?*/
short Reading;
void setup() {
  // put your setup code here, to run once:
  
  pinMode(LED_RED,OUTPUT);/*configuring the pin as an output pin*/
  pinMode(pot,INPUT);/*the  pin connected to the potentiometer in the ESP32 is an input pin*/
  Serial.begin(115200);
  Serial.println("Hello, ESP32!"); /*prints a message on the console to inform that the 
  processor got to the end of the setup function*/
}

void loop() {
 Reading =analogRead(pot);

Serial.print("Analog value = "); 
Serial.println(Reading);
/*displaying the value of the analog portion 
taken by the potentiometer*/

Serial.print("Voltage = ");/*displaying the voltage taken from the potentiometer*/
Serial.println(Reading*5/4095.0);
if((Reading*5)/4095.0>=3.5)/*if the voltage given to the input pin is greater than or equal to 3.5*/
{
  digitalWrite(LED_RED,HIGH);/*turning ON the LED*/
}
else
{
  digitalWrite(LED_RED,LOW);/*turning OFF the LED*/
}
delay(1000);/*keeps the state of the LED for a set period of time*/
}/*second code*/












#include <DHT.h>
#include <Adafruit_Sensor.h>

#define DHT_PIN 25
#define DHT_TYPE DHT22

DHT dht(DHT_PIN,DHT_TYPE);
float humidity,T_CEL,T_FAH,HIF,HIC;
void setup() {

  Serial.begin(115200);
  Serial.println(F("DHT Testing:")); /*prints a message on the console to inform that the 
  processor got to the end of the setup function*/
  dht.begin();
  
}

void loop() {
/*delay between consecutive reading sequences*/
delay(2000);
humidity= dht.readHumidity();/*reading the humidity*/
T_CEL=dht.readTemperature();/*reading the temperature in celsius*/
T_FAH=dht.readTemperature(true);/*reading the temperature in fahrenheit*/

if(isnan(humidity||isnan(T_CEL)||isnan(T_FAH)))/* a test case that if failed will end the program*/
{
  Serial.println(F("Failed to read from the DHT sensor"));
  return;
}
/*calculating the index for each temperature measurement system*/
HIF = dht.computeHeatIndex(T_FAH,humidity);
HIC = dht.computeHeatIndex(T_CEL,humidity,false);
/*printing the results*/
Serial.print(F("Humidity: "));
Serial.print(humidity);
Serial.print(F("% Temperature: "));
Serial.print(T_CEL);
Serial.print(F("*C "));
Serial.print(T_FAH);
Serial.print(F("*F Heat Index: "));
Serial.print(HIC);
Serial.print(F("*C"));
Serial.print(HIF);
Serial.println(F("*F"));
}/*third code*/
