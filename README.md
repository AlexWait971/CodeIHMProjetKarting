# CodeIHMProjetKarting
Le code du projet Kartind 2019/2020
extern uint8_t SmallFont[];
UTFT myGLCD(ITDB32S, 38, 39, 40, 41);
int tempPin = 0;
float tempC;

void setup()
{
  randomSeed(analogRead(0));

  // Setup the LCD
  myGLCD.InitLCD();
  myGLCD.setFont(SmallFont);
  myGLCD.clrScr();

  //km/h
  myGLCD.setColor(VGA_WHITE);
  myGLCD.fillRect(0, 0, 99, 19);
  
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawRect(0, 0, 99, 99);
  myGLCD.print("km/h", 33, 3);
  

  //température des batteries
  myGLCD.setColor(VGA_WHITE);
  myGLCD.fillRect(0, 99, 99, 135);
  
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawRect(0, 99, 99, 199);
  myGLCD.print("Temperature", 6, 103);
  myGLCD.print("Batt1", 5, 121);
  myGLCD.print("Batt2", 55, 121);
  
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawLine(49,136,49,199);
  
  myGLCD.setColor(VGA_BLACK);
  myGLCD.drawLine(49,119,49,135);
  
  myGLCD.setColor(VGA_BLACK);
  myGLCD.drawLine(1,119,98,119);
 
  // tr/min
  myGLCD.setColor(VGA_WHITE);
  myGLCD.fillRect(99, 0, 199, 19);
  
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawRect(99, 0, 199, 99);
  myGLCD.print("t/min", 127, 3); 

  // ligne de séparation entre km/h et t/min

  myGLCD.setColor(VGA_BLACK);
  myGLCD.drawLine(99,0,99,19);
 
  // Temperature moteur
  
  myGLCD.setColor(VGA_WHITE);
  myGLCD.fillRect(99, 99, 199, 119);
  
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawRect(99, 99, 199, 199);
  myGLCD.print("TMot", 132, 103);

  //thermistance
  
 
  

  //separation temp et tmot

  myGLCD.setColor(VGA_BLACK);
  myGLCD.drawLine(99,99,99,119);
 
  // Pourcentage batterie
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawRect(199, 0, 259, 199);
  myGLCD.print("%Bat", 213, 3);

  // puissance moteur
  myGLCD.setColor(VGA_WHITE);
  myGLCD.drawRect(259, 0, 319, 199);
  myGLCD.print("Pce", 280, 3);
  

  // Mode de conduite et temperatre exterieur
  myGLCD.setColor(VGA_WHITE);
  myGLCD.print("Mode de conduite:", 0, 202);
  myGLCD.print("Temperature exterieure:", 0, 220);

 
 
}
void loop() {

int tempReading = analogRead(tempPin);
  // This is OK
  double tempK = log(10000.0 * ((1024.0 / tempReading - 1)));
  tempK = 1 / (0.001129148 + (0.000234125 + (0.0000000876741 * tempK * tempK )) * tempK );       //  Temp Kelvin
  float tempC = tempK - 263.15;            // Convert Kelvin to Celcius
  myGLCD.setColor(VGA_WHITE);
  myGLCD.printNumF(tempC,2,136,160);
  delay(500);
  
}
