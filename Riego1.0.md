# P.P.Riego-Automatizado
Codigo de arduino (IDE)
int humedad = 0;
int agua = 0; 
int pulsado = 0;

void setup(){
 Serial.begin(9600);
 pinMode(12, OUTPUT);
 pinMode(9, OUTPUT);    
 pinMode(5, INPUT);      
 pinMode(3, INPUT);      
                         
}

void loop() {  
 if (digitalRead(3) == 1) { 
   pulsado = 1;
   digitalWrite(12, HIGH); 
 }
 pulsador();
}

void pulsador() { 
 int intensidad = analogRead (A0); 
 Serial.println("Intensidad: ");
 Serial.println(intensidad); 
 Serial.println("\n");
 delay(1000);
 if (pulsado == 1) { 
   if (intensidad > agua) { 
       delay(5000);    
       if (intensidad > agua){ 
         pulsado = 1;
         riego();
       }
     }else {
        digitalWrite(10, LOW); 
        //pulsado = 0;
      
        }
 }else {
   Serial.println("Pulsador: NO");}
}

void riego() {
     if (digitalRead(5) == 0) { 
         delay(2000);
         humedad = 0; 
         digitalWrite(9, HIGH); //
         delay(25000);
         digitalWrite(9, LOW); 
         delay(120000);
         riego();    
      }
      else {digitalWrite (9, LOW);
      humedad = 1; 

      }
}
