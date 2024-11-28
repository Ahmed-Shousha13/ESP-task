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

void setup() {
  // put your setup code here, to run once:
  pinMode(LED_RED,OUTPUT);/*configuring the pin as an output pin*/
  pinMode(pot,INPUT);/*the  pin connected to the potentiometer in the ESP32 is an input pin*/
  Serial.begin(115200);/*idk???*/
  Serial.println("Hello, ESP32!"); /*prints a message on the console to inform that the 
  processor got to the end of the setup function*/
}

void loop() {
short Reading =analogRead(pot);

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
