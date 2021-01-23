float vREF = 57;//output voltage refrence
int feedback_pin = A0;//the feedback input chip pin 3 
int PWM_pin = 1; //chip pin 5 portB pin 0 for pwm
int RED_LED = 3;
int GREEN_LED = 2;
int pwm_val;//inital value of the pwm
float voltageRead;
float vout;
float error = 0.2;
int timedelay = 10;
void setup() {
  // put your setup code here, to run once:
  pinMode(PWM_pin,OUTPUT);
  pinMode(GREEN_LED,OUTPUT);
  pinMode(RED_LED,OUTPUT);
  pinMode(feedback_pin,INPUT);
  TCCR0B = TCCR0B & 0b11111000 | 0b001;
  digitalWrite(PWM_pin, LOW);
  pwm_val = 1;
  analogReference(EXTERNAL);
}
void loop() {
  voltageRead = analogRead(feedback_pin);
  vout = voltageRead*(5/1090.0)*20;//mapping feedback voltage to the real value
  if( vout < vREF - error){ 
    pwm_val++;
    if (pwm_val == 255 )
    {
      pwm_val = 128;
      analogWrite(PWM_pin,pwm_val);
      
    }
    pwm_val = constrain(pwm_val,1,256);
  }
  if( vout > vREF + error){
    pwm_val--;
    pwm_val = constrain(pwm_val,1,256); 
  }
  if(pwm_val>=128)
  {
    digitalWrite(RED_LED,HIGH);
    digitalWrite(GREEN_LED,LOW);
  }
  if(pwm_val<128)
  {
    digitalWrite(RED_LED,LOW);
    digitalWrite(GREEN_LED,HIGH);
  }
  analogWrite(PWM_pin,pwm_val);
  delay(timedelay);

}
