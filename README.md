GSM Alert Code 

#include <SoftwareSerial.h>
SoftwareSerial SIM900(7, 8); // gsm pins tdx and rdx is connected to arduino pins 7 and 8
String textForSMS;
int smokes= A1; // mq9 senson pin a0 is connected to a1 pin of arduino
int data = 0; // first we are declaring the data as 0



void setup() {


=======
void setup() {

  randomSeed(analogRead(0));

  Serial.begin(9600);
 SIM900.begin(9600); // for sim 900a it is 9600

  pinMode(smokes, INPUT);

}

void loop() {
=======
  pinMode(smokes, INPUT); pinMode( Alert , INPUT);
}

void loop() {{

  data = analogRead(smokes); // Taking values from mq9 sensor and storing in data

  Serial.print("Smoke: ");
  Serial.println(data); // printing the values taken from sensor


	if ( data > 250) // limit for gas is given as 250
  {
	textForSMS =  "\nGas Or Smoke Detected";  // message to be sent if gas leaks
  sendSMS(textForSMS); // sendSMS function is called
  Serial.println(textForSMS);
  Serial.println("message sent.");
delay(5000);
while(1)
{

}
  }
}
=======



void sendSMS(String message)
{
  SIM900.print("AT+CMGF=1\r");                 	// It is the command to send SMS
  delay(1000);
 SIM900.println("AT + CMGS = \"+918142403340\"");  // Phone no to which msg to be sent

  delay(1000);
  SIM900.println(message);                    	
  delay(1000);
  SIM900.println((char)26);                   	
  delay(1000);
  SIM900.println();
  delay(100);                                 	// time to send sms
 // SIM900power();                                  
}
