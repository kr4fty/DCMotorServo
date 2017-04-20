DCMotorServo
============

An Arduino Library for controlling DC motors with rotary encoders. This library uses PID and Encoder feedback. It is modeled a little bit after the AccelStepper library.

 * Encoder Library, for measuring quadrature encoded signals from [FlexibleEncoder](https://github.com/kr4fty/FlexibleEncoder)
 * PID Library, for using encoder feedback to controll the motor from http://playground.arduino.cc/Code/PIDLibrary  also on [GitHub](https://github.com/br3ttb/Arduino-PID-Library)

Circuit
-------
I used a 754410 quad half-H controller (a pin-compatible L293D). I'm sure it would be cheaper to make out of other components, but i've never done transistor matching, and i'm afraid of burning things.

### Example circuit connections
<table>
<tr><td>L293D or 754410 pins</td><td>Device</td><td></td></tr>
<tr><td>1, 9</td><td>arduino</td><td>pin_pwm_output</td></tr>
<tr><td>2, 15</td><td>arduino</td><td>pin_dir</td></tr>
<tr><td>7, 10</td><td>arduino</td><td>pin_dir</td></tr>
<tr><td>4, 5, 12, 13</td><td>power</td><td>GND</td></tr>
<tr><td>16</td><td>power</td><td>5V</td></tr>
<tr><td>8</td><td>power</td><td>12V</td></tr>
<tr><td>3, 14</td><td>motor</td><td>motor pin 1</td></tr>
<tr><td>6, 11</td><td>motor</td><td>motor pin 2</td></tr>
</table>
  
Hardware
--------
 * [Metal Gearmotor 37Dx57L mm with 64 CPR Encoder from Pololu](http://www.pololu.com/catalog/product/1447)
 * Arduino
 * ~~754410 or L293D~~ [MC33926 Motor Driver Carrier](http://www.pololu.com/product/1212)
  
Pins
----
Pinout for motor control uses 3 pins for output. It is somewhat wasteful, but had more flexibility. Two pins for direction control, and one for motor power (assuming PWM).
Be sure to pick a PWM capable pin for pin_pwm_output.

The two input pins are for the encoder feedback.

Two direcional pins allow for setting a motor brake by shorting the terminals of the motor together (set both directions HIGH, and preferably turn off the PWM)

Update (by Kr4fty)
------------------
[FlexibleEncoder](https://github.com/kr4fty/FlexibleEncoder)library is used instead of [Encoder](http://www.pjrc.com/teensy/td_libs_Encoder.html).

This is because "Arduino ONE" only has two external interrupt pins and if you wanted to control two motors you would need two "arduino one", one for each encoder. To solve this, the Atmega chips have a special type of interrupts called "PIN CHANGE INTERRUPT" (PCINT) that allows you to have many more pins for interrupts (arduino one has 23 PCINT for example) but only has three interrupt vectors for all of them So you have to see which pin is really interrupting. This suggests that the "interruption" process is slower.

More information can be found here: https://www.avrprogrammers.com/howto/int-pin-change
  
TODO
----
 * implement brake feature for 3-pin mode
 * 2-pin constructor
 * implement friendlier tuning method for PID
