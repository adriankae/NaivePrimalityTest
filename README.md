# Naive primality test on Arduino with LCD Display
 

## Description

The Arduino checks in a range of 1 to \\(2^{32}-1\\) wether the number is a prime or not and counts the primes found until the current iteration.

The number of primes found and the largest prime found already will be displayed on the LCD.

You can watch your Arduino crunching numbers!

## Difficulty

This is a small and **very easy** beginner project for Arduino with LCD Display.

Requires moderate soldering skills.

## Parts list

I used the following parts:

* Arduino uno
* LCD 2x16
* pin headers to solder to the LCD
* 10k Poti
* 220 Ohm Resistor
* Jumper wires
* Breadboard

see also <https://www.arduino.cc/en/Tutorial/LiquidCrystalDisplay>

## Schematic

The schematic for hooking up the LCD to your Arduino can be found at <https://www.arduino.cc/en/Tutorial/LiquidCrystalDisplay>.

Or here (used from the website above, licensed by CC SA 3.0):  

![licensed by CC SA 3.0](https://github.com/adriankae/NaivePrimalityTest/blob/master/LCD_Base_bb_Fritz.png?raw=true "Circuit")

## Implementation

Pseudocode can be found at <https://en.wikipedia.org/wiki/Primality_test>.
My code is listed below in the code section.

## Code

	#include <LiquidCrystal.h>
	
	// initialize the library with the numbers of the interface pins
	LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
	unsigned long primeCount = 0; // for counting primes found so far
	unsigned long i = 1; // iterator for primes
	
	char isPrime(long n){
	  if(n < 1){ // primes are >0 by definition
	    return 0;
	  }
	  else if(n <= 3){ // 1,2,3 are primes
	    return 1;
	  }
	  else if( ( (n % 2) == 0) || ( (n % 3) == 0)){ // checking for 2 actually 
	  												//obsolete because of (i + 2)
	    return 0;
	  }
	
	  unsigned long divisor = 5;
	  while(divisor*divisor <= n){ // check all divisors, 
	    if( ( (n % divisor) == 0) || ( (n % (divisor + 2)) == 0)){
	      return 0;
	    }
	    divisor += 6;
	  }
	  return 1;
	}
	
	
	void setup() {
	  // set up the LCD's number of columns and rows:
	  lcd.begin(16, 2);
	  lcd.print("Primality test"); 
	  delay(2000); 
	}
	
	void loop() {
	  if(isPrime(i)){
	    if(i <= 4294967295 ){ // prevents loop from counting higher 
	    					  //after reaching the limits of unsigned long
	      primeCount++;
	    }
	    lcd.clear();
	    lcd.setCursor(0,0);
	    lcd.print("c: ");
	    lcd.setCursor(2,0);
	    lcd.print(primeCount);
	    lcd.setCursor(0,1);
	    lcd.print(i);
	  }
	  if(i <= 4294967295 ){ // keeps loop within the limits of unsigned long
	    i += 2;  
	  }
	}
	
## Pictures

![](https://github.com/adriankae/NaivePrimalityTest/blob/master/DSC_0048.JPG?raw=true"")
![](https://github.com/adriankae/NaivePrimalityTest/blob/master/DSC_0052.JPG?raw=true"")

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

