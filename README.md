VarSpeedServoSam
===============

The VarSpeedServoSam Arduino library is an adaptation of the [VarSpeedServo.h](https://github.com/netlabtoolkit/VarSpeedServo) library to work on boards with SAM processor such as Arduino Due. The original VarSpeedServo.h which is developed by @netlabtoolkit allows the use of up to 8 servos moving asynchronously (because it uses interrupts). In addition, you can set the speed of a move, optionally wait (block) until the servo move is complete, and create sequences of moves that run asynchronously.

* Supports up to 8 servos
* Allows simultaneous, asynchronous movement of all servos
* The speed of a move can be set
* The write() function initiates a move and can optionally wait for completion of the move before returning
* A servo can be sent a sequence of moves (where each move has a position and speed)

Sample Code
----------------------------

```

#include <VarSpeedServoSam.h> 
 
VarSpeedServoSam myservo;    // create servo object to control a servo 
 
void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object 
} 
 
void loop() {
  myservo.write(180, 30, true);        // move to 180 degrees, use a speed of 30, wait until move is complete
  myservo.write(0, 30, true);        // move to 0 degrees, use a speed of 30, wait until move is complete
}
```

Additional examples are included in the distribution and are available in the Arduino Examples section.

API
================

A servo is activated by creating an instance of the Servo class passing the desired pin to the attach() method. The servos are pulsed in the background using the value most recently written using the write() method
 
VarSpeedServoSam - Class for manipulating servo motors connected to Arduino pins. Methods:

	attach(pin )  - Attaches a servo motor to an i/o pin.
	attach(pin, min, max  ) - Attaches to a pin setting min and max values in microseconds
	default min is 544, max is 2400  

	write(value)     - Sets the servo angle in degrees.  (invalid angle that is valid as pulse in microseconds is treated as microseconds)
	write(value, speed) - speed varies the speed of the move to new position 0=full speed, 1-255 slower to faster
	write(value, speed, wait) - wait is a boolean that, if true, causes the function call to block until move is complete

	writeMicroseconds() - Sets the servo pulse width in microseconds 
	read()      - Gets the last written servo pulse width as an angle between 0 and 180. 
	readMicroseconds()  - Gets the last written servo pulse width in microseconds. (was read_us() in first release)
	attached()  - Returns true if there is a servo attached. 
	detach()    - Stops an attached servos from pulsing its i/o pin. 

	slowmove(value, speed) - The same as write(value, speed), retained for compatibility with Korman's version

	stop() - stops the servo at the current position

	sequencePlay(sequence, sequencePositions); // play a looping sequence starting at position 0
	sequencePlay(sequence, sequencePositions, loop, startPosition); // play sequence with number of positions, loop if true, start at position
	sequenceStop(); // stop sequence at current position

Installation
=============

* Download the .zip file from the releases section of GitHub
* In Arduino, select SKETCH>IMPORT LIBRARY...>ADD LIBRARY... and find the .zip file
* This will install the library in your My Documents (Windows) or Documents (Mac) folder under Arduino/libraries
* You can also unzip the file, and install it in the above libraries folder manually
* See [arduino.cc/en/Guide/Libraries](http://arduino.cc/en/Guide/Libraries) for more info on libraries

Acknowledgement
=============

As said before, this library is based on VarSpeedServo.h which is developed by @netlabtoolkit and Arduino standard servo library. Many thenks to those developers.
