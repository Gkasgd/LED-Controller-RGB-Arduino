LED-Controller-RGB-Arduino
==========================
const int BotonPin1 = 3; // Pin 3 Botón 1

const int BotonPin2 = 4; // Pin 4 Botón 2

const int BotonPin3 = 5; // Pin 5 Botón 3

const int BotonPin4 = 6; // Pin 6 Botón 4

const int RojoPin = 9;  //Pin 9 para controlar Rojo

const int VerdePin = 10;//Pin 10 para controlar Verde

const int AzulPin = 11;//Pin 11 para controlar Azul

 // Variables booleanas para control de rebote y accionar de los botones

boolean ultimoEstado1 = LOW;
boolean ultimoEstado2 = LOW;
boolean ultimoEstado3 = LOW;
boolean ultimoEstado4 = LOW;

boolean estadoActual1 = LOW;
boolean estadoActual2 = LOW;
boolean estadoActual3 = LOW;
boolean estadoActual4 = LOW;

//Variable de enteros o integer que vá a manejar sólo hasta 255, que es el máximo de i, intensidad, que vá a manejar el led

int ir = 0;
int ig = 0;
int ib = 0;
int i = 0;

void setup() {

// Inicialización de botones como INPUT
  
  pinMode(BotonPin1, INPUT);
  pinMode(BotonPin2, INPUT);
  pinMode(BotonPin3, INPUT);
  pinMode(BotonPin4, INPUT);
  
// Inicialización de LEDs
  
  pinMode(RojoPin, OUTPUT);
  pinMode(VerdePin, OUTPUT);
  pinMode(AzulPin, OUTPUT);
}
// Funcion anti rebote en botones mecánicos.

boolean debounce(boolean ultimo, int BotonPin)
{
  boolean actual = digitalRead(BotonPin);
  if (ultimo != actual)
  {
    delay(5);
    actual = digitalRead(BotonPin);
  }
  return actual;
}

void loop()
{
  estadoActual1 = debounce(ultimoEstado1, BotonPin1);
  estadoActual2 = debounce(ultimoEstado2, BotonPin2);
  estadoActual3 = debounce(ultimoEstado3, BotonPin3);
  estadoActual4 = debounce(ultimoEstado4, BotonPin4);
  
  if (ultimoEstado1 == LOW && estadoActual1 == HIGH)
  {
    ir = ir + 51;
  }
  ultimoEstado1 = estadoActual1;
  
  if (ultimoEstado2 == LOW && estadoActual2 == HIGH)
  {
    ig = ig + 51;
  }
  ultimoEstado2 = estadoActual2;
  
  if (ultimoEstado3 == LOW && estadoActual3 == HIGH)
  {
    ib = ib + 51;
  }
  ultimoEstado3 = estadoActual3;
  
  if (ultimoEstado4 == LOW && estadoActual4 == HIGH)
  {
    i = i + 51;
  }
  ultimoEstado4 = estadoActual4;
  
  if (ir > 255) ir = 0;
  if (ig > 255) ig = 0;
  if (ib > 255) ib = 0;
  if (i > 255) i = 0;
  
  analogWrite(RojoPin,ir);
  analogWrite(VerdePin,ig);
  analogWrite(AzulPin,ib);
