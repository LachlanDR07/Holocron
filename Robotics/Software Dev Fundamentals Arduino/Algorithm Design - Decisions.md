---
tag: Robotics
---

![[Theory#Algorithm Design - Decisions]]


# Arduino Implementation
## IF..THEN..

In Arduino, as with many other languages, the main decision block is the `IF..THEN..`. The syntax for this in Arduino is:

![[Screen_Shot_2021-12-16_at_2.07.37_pm.png|Screen Shot 2021-12-16 at 2.07.37 pm.png]]

<aside>
💡 Note the condition is enclosed in parenthesis.

</aside>

For the code block to execute, the condition needs to equate to **true**. If the condition equates to **false**, the code block is skipped.

### IF..THEN.. Example

```arduino
if (x > 120) {
  digitalWrite(LEDpin1, HIGH);
  digitalWrite(LEDpin2, HIGH);
}
```

In this example, `x > 120` is the condition and `digitalWrite(LEDpin1, HIGH);
  digitalWrite(LEDpin2, HIGH);` is the code block that will run only if the condition is true at the time it is executed.

## IF..THEN.. ELSE..

![[Screen_Shot_2021-12-16_at_2.28.59_pm.png|Screen Shot 2021-12-16 at 2.28.59 pm.png]]

The standard IF..THEN structure can be extended with an ELSE to allow a code block to run if the condition is false.

### IF..THEN..ELSE.. Example

```arduino
if (x > 120) {
  digitalWrite(LEDpin1, HIGH);
  digitalWrite(LEDpin2, HIGH);
} else {
	digitalWrite(LEDpin1, LOW);
  digitalWrite(LEDpin2, LOW);
}
```

In this case, if x is greater than 120, then the LEDs will be turned on. If x is NOT greater than 120, the LEDs will turn off.

## Switch ... Case

Switch cases are a different type of control structure to replace multiple, nested if..then statements. 

Based on a given variable, Arduino code can have multiple cases or a catch-all state - default. They can be used to simplify code, but still provide multiple cases for variables.

### Syntax

```arduino
switch (var) {
  case label1:
	// statements
	break;
  case label2:
	// statements
	break;
  default:
	// statements
	break;
}
```

### Example

```arduino
x = random(5);
switch (x) {
	  case 0: y = y + 1;
	  case 1: y = y + 5;
	  case 2: y = y + 2;
	  case 3: y = y + 7;
	  case 4: y = y + 3;
	  default: y = 0;
	}

// Compared to the equivalent IF statements:
if (x == 0) y = y + 1;
	else if (x == 1) y = y + 5;
	else if (x == 2) y = y + 2;
	else if (x == 3) y = y + 7;
	else if (x == 4) y = y + 3;
	else y = 3;
```

## **Comparison Operators**

The standard *comparison* operators in Arduino are shown here and can be used in `if` conditions.

| Operator | Description |
| --- | --- |
| `!` | Not |
| `x == y` | x is equal to y |
| `x != y` | x is not equal to y |
| `x < y` | x is less than y |
| `x > y` | x is greater than y |
| `x <= y` | x is less than or equal to y |
| `x >= y` | x is greater than or equal to y |

## Logical Operators

| Operator | Description | Example |
| --- | --- | --- |
| && | AND  |  |
| || | OR |  |
| ! | NOT |  |

# Practical Exercises

<aside>
‼️ **Goal**

In this task, you’ll be updating the Bank Alarm Project to :

- include decision making, specifically to check if the potentiometer has reached a certain value (threshold) before the LED turns on.
- You’ll then add additional components to build the final form of the Bank alarm which will operate under the following conditions:
	- 3 of the Sensors must be “triggered” for the alarm to go off (LED turn on)
</aside>

Open the Bank Alarm project on [Tinkercad](https://www.tinkercad.com/). Before implementing decisions specifically in the code, some code base changes need to be made to reorganise the code. 

## Modifying the Circuit

In this stage, the code will not be changed, only the circuit itself. Close out of the Code view by clicking the code button in the tool bar.

![[Untitled 3.png|Untitled]]

Change the component list to **Components Basic** in the dropdown list.

![[Untitled 4.png|Untitled]]

Delete the ‘wires’ connecting the LED to the arduino and resistor. Select the wire and press delete.

![[Untitled 5.png|Untitled]]

Add a **Breadboard Small** to the circuit by dragging the component to the circuit area.

![[Jan-12-2023_15-05-35.gif|Jan-12-2023 15-05-35.gif]]

Move the resistor and LED over to the new breadboard. 

![[Untitled 6.png|Untitled]]

Connect a wire from the **Anode** pin (on the right) to the top of the resistor. Do this by clicking on the Anode and then clicking on the top terminal of the resistor.

![[Jan-12-2023_15-12-07.gif|Jan-12-2023 15-12-07.gif]]

Connect the bottom terminal of the resistor to the breadboard.

![[Jan-12-2023_15-13-15.gif|Jan-12-2023 15-13-15.gif]]

### Breadboards

A breadboard is a reusable platform used for building and prototyping electronic circuits. It allows you to easily connect and disconnect components, without having to solder them together. Breadboards consist of a grid of holes into which electronic components can be inserted. The holes are typically arranged in a pattern of interconnected vertical and horizontal rows. This allows for the connection of different components' leads, such as resistors, capacitors, and transistors, to be easily connected together to create a functioning circuit.

![[Untitled 7.png|Untitled]]

![[Untitled 8.png|Untitled]]

Connect the **Cathode** pin of the LED to the **Black** (- or ground) ****rail of the breadboard.

Using the toolbar, change the colour of the Ground wire to black. This is the standard for Ground wires in wiring diagrams.

![[Untitled 9.png|Untitled]]

Next, connect the Ground rail on the breadboard to the GND pin on the Arduino. Then, connect the Positive (red) rail on the breadboard to the 5V pin.

You can set corners in the wires by double clicking at the point you want to add a bend.

![[gnd.gif|gnd.gif]]

![[Jan-12-2023_15-25-29.gif|Jan-12-2023 15-25-29.gif]]

Finally, connect Pin 9 on the Arduino to the same row that your resistor is connected to.

![[Jan-12-2023_15-29-27.gif|Jan-12-2023 15-29-27.gif]]

<aside>
‼️ Make sure the wire is connected to the correct row as your resistor.

![[Untitled 10.png|Untitled]]

</aside>

Run and test your code to ensure that the wiring is correct!

Move the potentiometer and reconnect it through the breadboard.

Also, connect the bottom 5V rail to the 5V pin, and the bottom GND (-) rail to the GND pin.

<aside>
‼️ Remember that when rewiring the potentiometer, you’ll need to wire the potentiometer pins to the correct Arduino pins.

| Pot Pin | Connect to | Description |
| --- | --- | --- |
| 1 | 5V | Positive Power |
| 2 | A0 | Data or Signal |
| 3 | GND | Negative (Ground) Power |

![[Untitled 11.png|Untitled]]

</aside>

Your circuit should now appear similar to this. Not the Data pin connected through the breadboard - ensure that the wires are connected on the same row.

![[Untitled 12.png|Untitled]]

### Additional Sensors

Add two more components to the circuit - the first is a **Ultrasonic Distance** (Sonar) sensor, and the second is a **Passive InfraRed** Sensor. 

- A Ultrasonic Distance sensor can detect distance to objects but sending out a pulse signal and timing how long it takes for the signal to bounce back.
- A Passive Infrared (PIR) sensor detects movement.

Drag out the two components and wire them through the breadboard. Connect the 5V pins to the positive (red) rail, and the Ground pins to the negative (black) rail.

<aside>
‼️ There are two ultrasonic sensors in the library. The one you want for this circuit is the one with **four** pins and has **HC-SR04** written on the image
You may need to change the component listing to **All** to find the correct Ultrasonic sensor.

![[Untitled 13.png|Untitled]]

</aside>

![[Untitled 14.png|Untitled]]

Connect the Signal pin of the PIR sensor to Pin 2 through the breadboard.

![[Untitled 15.png|Untitled]]

Connecting the Sonar sensor requires connecting two wires to the Arduino. 

- **Trig** pin for sending the pulse. Connect this to pin 3.
- **Echo** for reading the response of the pulse. Connect this to pin 11.

![[Untitled 16.png|Untitled]]

## Code Reorganisation

Create a new function to handle the functionality that is being implemented.

![[Untitled 17.png|Untitled]]

```arduino
void determineLEDBrightness(int brightnessValue) {
  
}
```

Update `loop()` to call this function **instead** of `setLEDBrightness()`.

<aside>
‼️ This new function is now going to act as intermediately between the main loop functionality and making the decision whether to turn the LED on or not, before setting the brightness.

</aside>

![[Untitled 18.png|Untitled]]

Change the argument for calling  `determineLEDBrightness` to be `potReading` instead of `brightness`.

![[Untitled 19.png|Untitled]]

Add `//` to the front of the line of code which maps the brightness variable.

<aside>
‼️ This **comments** out the line of code, removing it from compilation and execution - essentially, the line of code is ignored by the computer.

</aside>

![[Untitled 20.png|Untitled]]

## Decision Making - LEDs

Now the code has been reorganised, it’s time to focus on the new functionality - the LED is turned on until a particular potentiometer value is reached, then the brightness of the LED is determined by the remainder of the values.

For simplicity, the threshold value of 511 is used here - half way between 0 and 1023. If the potentiometer reads under and including 511, the LED will remain off, over 511, the LED brightness will be scaled.

Create a new variable inside `determineLEDBrightness()` to store the value that is determined.

![[Untitled 21.png|Untitled]]

```arduino
int brightness;
```

In `determineLEDBrightness()`, add an `if` statement to check `brightnessValue`.

![[Untitled 22.png|Untitled]]

```arduino
if (brightnessValue <= 511) {
	
}
```

If the condition is **true** then the LED needs to be turned off. This is done by setting the value of `brightness` to 0.

![[Untitled 23.png|Untitled]]

```arduino
brightness = 0;
```

Add an `else` clause to handle any values greater than 511.

![[Untitled 24.png|Untitled]]

Now, the mapping can be done. This is similar to how it was previously done in `loop()` however you don’t need to calculate for values 0-511 as these values have already been handled.

![[Untitled 25.png|Untitled]]

```arduino
brightness = map(brightnessValue, 512, 1023, 0, 255);
```

Finally, outside of the `if` block, write the `brightness` value to the LED pin by passing it to `setLEDBrightness()`.

![[Untitled 26.png|Untitled]]

```arduino
setLEDBrightness(brightness);
```

## Test the functionality

Start the simulation and you should see the new functionality in the circuit.

![[Jan-12-2023_11-29-44.gif|Jan-12-2023 11-29-44.gif]]

### Final Code

```arduino
const int pinLED = 9;
const int pinPot = A0;

void setup()
{
  pinMode(pinPot, INPUT);
  pinMode(pinLED, OUTPUT);
  Serial.begin(9600);
}

void loop()
{
  int potReading = readPotentiometer();
  //int brightness = map(potReading, 0, 1023, 0, 255);
  determineLEDBrightness(potReading);
  delay(250);
}

int readPotentiometer() {
  int potValue = analogRead(pinPot);
  Serial.println(potValue);
  return potValue;
}

void determineLEDBrightness(int brightnessValue) {
  int brightness;
  if (brightnessValue <= 511) {
	brightness = 0;
  } else {
	brightness = map(brightnessValue, 512, 1023, 0, 255);
  }
  setLEDBrightness(brightness);
}

void setLEDBrightness(int LEDBrightness) {
  analogWrite(pinLED, LEDBrightness);
}
```

## Decision Making - Multiple Inputs

In this stage, the circuit will take inputs from multiple sensors ( Potentiometer, Sonar and PIR) and determine whether the LED should be on or not.

Define constants for the pins being used. These are to be set at the start of the code.

![[Untitled 27.png|Untitled]]

```arduino
const int trigPin = 3;
const int echoPin = 11;
const int pinPIR = 2;
```

Add the code in `setup()` to configure the pins to be input or output.

![[Untitled 28.png|Untitled]]

```arduino
pinMode(trigPin, OUTPUT); // Sets the trigPin as an OUTPUT
  pinMode(echoPin, INPUT); // Sets the echoPin as an INPUT
  pinMode(pinPIR, INPUT); // Sets the trigPin as an OUTPUT
```

Add a function to read the response from the PIR.

The PIR sensor responds with `true` if it detects movement, `false` otherwise.

![[Untitled 29.png|Untitled]]

```arduino
boolean readPIR() {
 return digitalRead(pinPIR);
}
```

Add the following function to utilise the Sonar sensor.

This function does all the specific low-level code to send the pulse and read the response from the sonar. 

If the distance to the object is determined to be less than the threshold, then the function returns `true`, otherwise `false`.

![[Untitled 30.png|Untitled]]

```arduino
boolean readDistance(int distanceThreshold) {
  long duration; // variable for the duration of sound wave travel
  int distance; // variable for the distance measurement
   // Clears the trigPin condition
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  // Sets the trigPin HIGH (ACTIVE) for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  // Calculating the distance
  distance = duration * 0.034 / 2; // Speed of sound wave divided by 2 (go and back)
  // Displays the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  if (distance < distanceThreshold) {
	return true;
  } else {
	return false; 
  }
}
```

To help the debugging process that may be required in the future, add a helper function which outputs all the values of the sensors. This will help you determine if and when there are any problems with the alarm triggering.

<aside>
‼️ Adding this as a function will allow this to be easily turned on and off by removing the function call.

</aside>

![[Untitled 31.png|Untitled]]

```arduino
void debugSensors(int potValue, boolean pirValue, boolean sonarValue) {
  Serial.print("The potentiometer value is :"); 
  Serial.print(potValue);
  Serial.print(". The PIR Reads:");
  Serial.print(pirValue);
  Serial.print(". The Sonar Reads:");
  Serial.println(sonarValue);
}
```

Create a function that will access and read the sensor values from the functions created previously.

This function reads the responses from all the other functions and stores them locally.

![[Untitled 32.png|Untitled]]

```arduino
void triggerAlarm() {
  int potTrigger = readPotentiometer();
  boolean pirTrigger = readPIR();
  boolean sonarTrigger = readDistance(100);
  debugSensors(potTrigger, pirTrigger, sonarTrigger);
}
```

Add an if statement to determine if all three trigger values are ‘correct’. “Correct” in this case means that they are enough to meet the requirements to trigger the alarm - the potentiometer value needs to be greater than 511. The PIR and Sonar values need to be `true`.

![[Untitled 33.png|Untitled]]

```arduino
if (potTrigger > 511 && pirTrigger == true && sonarTrigger == true) {
	
} else {
	
}
```


> [!info]- **Compound** conditions
> Compound conditions such as the one shown above, a logical expression that combines multiple individual conditions using logical operators such as "and" (`&&`) or "or" (||). These conditions are typically used in control flow statements such as "if-else" or "while" loops to determine the execution of certain code. For example, the expression "`x > 0 && x < 10`" is a compound condition that checks whether the variable "x" is greater than 0 and less than 10. If both conditions are true, the code within the corresponding control flow statement will be executed.
> In the code shown, ALL of the individual conditions (red, yellow and purple) must equate to `true` for the whole `if` statement to be evaluated as `true`.
![[Untitled 34.png|Untitled]]



Add the appropriate code in the different if blocks to turn the LED on or off.

![[Untitled 35.png|Untitled]]

```arduino
if (potTrigger > 511 && pirTrigger == true && sonarTrigger == true) {
	Serial.println("Alarm Triggered");
	determineLEDBrightness(potTrigger);
  } else {
	Serial.println("Alarm Off");
	determineLEDBrightness(false);
  }
```

Finally, modify `loop()` to call `triggerAlarm()` instead of `determineLEDBrightness()`.

![[Untitled 36.png|Untitled]]

```arduino
void loop()
{
  int potReading = readPotentiometer();
  //determineLEDBrightness(potReading);
  triggerAlarm();
  delay(250);
}
```

## Test the functionality

Start the simulation and check to make sure that all three sensors need to have ‘correct’ values for the LED to be on.

![[Jan-13-2023_10-59-19.gif|Jan-13-2023 10-59-19.gif]]

**Sonar**

The highlighted value needs to be less than 100.

![[SCR-20230113-f6h.png|SCR-20230113-f6h.png]]

**Potentiometer**

The dial needs to be set to a value on the lefthand side (<511)

![[Untitled 37.png|Untitled]]

**PIR**

This sensor requires movement, so click on it and move the circle around. You’ll notice that when the sensor detects movement, it highlights in red on the sensor.

![[Jan-13-2023_10-54-17.gif|Jan-13-2023 10-54-17.gif]]

If the LED does not turn on as expected, check the Serial Monitor for the variable outputs to diagnose where the issue may reside.

![[Jan-13-2023_11-00-07.gif|Jan-13-2023 11-00-07.gif]]

# Extension Exercises

Using TinkerCAD, design the circuit and write code to:

1. Have LED on while a button is being pressed.

For this, you will need to identify the pins and set them to input or output in the `setup()` function. In the `loop()` function, read the value of the button using `digitalRead()`. If the button is pressed down, turn the LED on (digitalWrite HIGH). If the button is not being pressed, then turn the LED off (digitalWrite LOW).

![[2021-12-16_14-45-01.2021-12-16_14_45_46.gif|2021-12-16 14-45-01.2021-12-16 14_45_46.gif]]

1. When a button is pressed, turn the LED on for 1 second, and then off. (similar to Blink). 
2. Using the same circuit design, when the button is pressed, the LED turns on, and when pressed again, it is turned off. Google “StateChangeDetection Arduino”. This will assist.

1. Build this circuit. The sensor at the bottom is called a “potentiometer”, which is an analog input device. Use the code as a starting point. Continue writing the loop() function to complete the following logic:
`If the input from the potentiometer is above the threshold value, then turn the LED on. If it’s below the threshold, then turn the LED off.`

![[Screen_Shot_2022-02-15_at_7.33.21_am.png|Screen Shot 2022-02-15 at 7.33.21 am.png]]

```arduino
// These constants won't change:
const int analogPin = A0;    // pin that the sensor is attached to
const int ledPin = 13;       // pin that the LED is attached to
const int threshold = 400;   // an arbitrary threshold level that's in the range of the analog input

void setup() {
  // initialize the LED pin as an output:
  pinMode(ledPin, OUTPUT);
  // initialize serial communications:
  Serial.begin(9600);
}

void loop() {
// read the value of the potentiometer:
  int analogValue = analogRead(analogPin);
}
```

# Review

1. Describe a decision in programming using plain language.
	1. Update the sentence with more technical language. 
2. What’s a nested if statement?
3. What’s the difference between a nested if block and a case switch?
4. What logic gates or circuits can be found in the “StateChangeDetection Arduino” code?
