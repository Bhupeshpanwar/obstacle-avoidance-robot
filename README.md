##Hi! This is the description about obstacle avoidance robot 


##Objective:- Create an robot which can avoid obstacles using ultrasonic sensor.

##Apparatus:-arduino uno(you can also use arduino nano or other microcontroller), robo chassis, ultrasonic sensor(HC-SR04), 2x cell holders, 4 lithium ions cells 3.7 volts,motor driver L298N , servo motor(optional:- If you want that ultrasonic sensor scan whole surrounding/my code is only scanning front)
some glue and nut bolts, 4x dc shaft motors, 4 wheels

##Procedure:-1.Connect 2x motors of right side with parallel connection(you can series but do it parallel for better performance) and connect 2x motors of left side with parallel connection 

2. There are four output pins in L298N motor driver OUT1, OUT2, OUT3, OUT4. vcc pin ranging from 12 to 30v , gnd and 5v output pin (optional:- you can power your arduino from this but not recommended).and 4 input pins IN1,IN2,IN3,IN4 and two pwn pins ENA,ENB for speed control

3. The most important part in robot is Arduino uno(brain of the robot). powersupply recommended(5 to 20v DC)

4. now about power supply. Put 2x 3.7 volt in cell holder and other 2 with other cell holder. now you have 2  7.4 voltage power(3.7x2 = 7.4V), Now connect the cell holder with cell in
parallel connectionn ( why parallel??  The answer is cells in parallel increase mAh. if you have already high mAh . you can also connect in series then no issue and elsewise i have low vol
-tage dc motors so for me 7.4 volt is enough)

5.Now connect 2x motor on right side with OUT1,OUT2 and other 2x motor on left side with OUT3, OUT4. 

6.Here comes the input pins struggle connect  IN1, IN2,IN3,IN4 with arduino digital pins. 

7.But connect ENA/ENB pin with arduino digital pin with pwm(like digital pins with sign '~' like this ). they are used to control the speed(Note:- dont forget to remove the clip around ena/enb pins if have)

8. now give power supply to Hc-SR04(ultrasonic sensor) recommmended power supply(3.3v to 5v dc)
9. connect TRIG and ECHO pin with arduino digital pins

10. Note down all pin number carefully before procedding to code.
    
11. Now connect arduino with laptop/or your respective system

 12. open arduino ide and write your code ( i will share mine)

 13. Here is the code
 14. ##Code
 15. ```cpp
     #include <Servo.h>

     // Motor pins
    const int ENA = 5;
    const int IN1 = 2;
    const int IN2 = 3;

    const int ENB = 6;
    const int IN3 = 4;
    const int IN4 = 7;

    const int motorSpeed = 75;

    // Ultrasonic pins
    const int trigPin = 10;
    const int echoPin = 11;

    // Servo setup (optional, currently unused)
    Servo myServo;
    const int servoPin = 9;

    void setup() {
    pinMode(ENA, OUTPUT);
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
  
    pinMode(ENB, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);

    // Ultrasonic setup
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);

    // Optional: center servo if needed
    //myServo.attach(servoPin);
    //myServo.write(90);
    }

    void loop() {
    long distance = getDistance();

    if (distance > 15) {
    forward();
    } else {
    stopMotors();
    delay(300);       // Small pause before turning
    turnRight();
    delay(500);       // Time to complete the right turn
    stopMotors();
    delay(300);       // Small pause after turning
    }

    delay(100);  // Delay to avoid bouncing
    }

    // Move forward
    void forward() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);

    digitalWrite(IN3, HIGH);
    digitalWrite(IN4, LOW);

    analogWrite(ENA, motorSpeed);
    analogWrite(ENB, motorSpeed);
    }

    // Stop motors
    void stopMotors() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);

    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);

    analogWrite(ENA, 0);
    analogWrite(ENB, 0);
    }

    // Turn right (left motor moves forward, right motor stops or moves backward)
    void turnRight() {
    digitalWrite(IN1, HIGH);
    digitalWrite(IN2, LOW);

    digitalWrite(IN3, LOW);
    digitalWrite(IN4, HIGH); // Reverse right motor for sharper turn

    analogWrite(ENA, 100);
    analogWrite(ENB, 100);
    }

    // Measure distance using ultrasonic sensor
    long getDistance() {
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);

    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    long duration = pulseIn(echoPin, HIGH);
    long distance = duration * 0.034 / 2; // Convert to cm

    return distance;
    }

##Precautions:-
1.Also check power supply of all components throught their datasheets
2.do check code and the pin numbers


##Result:-
here is the video of my project
 https://youtube.com/shorts/Wkgs1-5DZQ8?si=g5a1SoIylWFBgC3I


 Thank you !!!

