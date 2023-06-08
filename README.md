# Robot Arm


* [Intro](#intro)
* [Planning](#planning)
* [Visuals](#visuals)
* [Code](#code)
* [Wiring](#wiring)
* [Reflection](#reflection)

---


## Intro
This project was based around the idea of PID and our task was to build a system using PID to keep one variable in the system constant. We decided to do a aquaponics system with the controlled variable being the water level of the plant tank. Our system would be relatively simple, the entire system would be essentially enclosed inside a large 20 gallon fish tank. The tank would be partially filled with water that would act as a reservoir their would then be a smaller water tank inside that would have its water level controlled via a pump and valve using PID.



## Planning 
 ### Goal
 Our goal was to make a small water tank hold a constant water level so that we could grow plants inside. 

 ### criteria 
 We had to make a PID system and for us that meant PIDing using valves and pumps to keep the water level of a small tank.
 
  ### success statement
  This project will be successful if the water level is constant enough to keep an aquaponics system afloat (pun intended).  

  ### planning documentation
our planning was rather simple as the main construction of our project was largely already made. The below pictures are our initial very rough sketch of the basis of our project, it will make much more sense once one views the completed project. The sketchs are faithful to our final project with the exception of the monitored tank being suspended instead of laying on some wood on the bottom 

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/14a5ad63-bd11-4430-85fb-e59f7401c26c" height="200">


<img src="https://github.com/cprocino/Aquaponics/assets/71406784/925c8a53-bd52-4210-a16a-6adc7ba785c8" height="200">

### Schedule 

our planning was slightly skewed by our knowledge of our lack of knowledge in PID 
for the first week after we decided on our project we would create the skeleton of our project using the fish tank and a few other household and lab items.
the rest of the time we would spend trying to figure out how we would PID the project and how the new valves and pumps could be controlled with arduinos. 
our initial plan was 

* week 1: build the basics of the tank with a pump and the correct tubing and a controllable valve or pump to regulate water level

* week 2: tweek pump and valve to maintain water level better(start with hand controls for PID)

* week 3: start implementing PID

* week 4-5: PID tuning

* week 6: finish documentation and add plants

### bill of materials 
* 1x 20 gallon fish tank

* 1x tupperware container

* 4x blocks of wood (for spacing)

* 1x arduino metro

* 1x ultrasonic sensor

* 1x battery pack 

* 1x breadboard 

* 1x 12 volt relay           

* 1x 5w submersible pump 

* 1x 12 volt 3 gpm valve








## Visuals
<img src="https://github.com/cprocino/Aquaponics/assets/71406784/86a0e908-96a6-4de7-9fcf-735391fd2e29" height="300">

This is a partial picture of our wiring that shows the most important parts ( see wiring diagram for full wiring) 

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/e2a363ca-2033-448c-b5bb-e4b3e986a802" height="300">

This is the board we cut out in order to make this a viable system for Hydro/aquaponics, it allows us to suspend potatoes in the water and lets them grow. 

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/a56aafc4-da36-4c78-8105-d22c0ad17798" height="300">

This is a picture of our small monitiered tank and the valve we used to affect flow.

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/99353b00-bdc5-4b77-abb7-96275dfcf8e0" height="250">

this is the tank that encloses the whole system

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/e11dadc4-419e-4fe5-b15d-2721fd8b6252" height="250">

this is our final pump, the one we first used was to strong and the valve could not keep up with the flow

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/ceef106a-32a8-4821-ae7c-09107d3ca763" height="250">

This is the whole project assembled without the water or plants. 

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/45a71b2f-20c6-462a-8690-de35b9570bf4" height="250">

This is the final pump we decided on, we got it from disassembling a small fish tank filter 


<img src="https://github.com/cprocino/Aquaponics/assets/71406784/c0a0b5c2-0847-4fc3-a14b-1832fafcfa8e" height="250">
 
 this is the pile of unused or discarded materials, stars of the show include two valves ordered from amazon that needed far more pressure than we had and  dozens of feet of tubing that turned out to be useless. 


<img src="https://github.com/Ncrawfo72/aquaponics/blob/main/images/aquaponics%20working.gif" height="450">

this is a video of it working.


## Wiring 

This is our wiring, it is not overly complex but it gets the job done:


<img src="https://github.com/cprocino/Aquaponics/assets/71406784/ab2396e1-eb2b-4488-9088-078385f6d8b5" height="400">

This is our white board wiring diagram, some comments are; the sensor is a hcsor04 ultrasonic sensor and valve is a needed 12 volts to open. 




<img src="https://github.com/cprocino/Aquaponics/assets/71406784/e2b536a0-490c-4253-8386-be21ea5720ce" height="350">



  

## Code



this was the PID that code is in our final version is as follows:
~~~python
   //*
   chris and nixon
   jun 1 2023
   this code is for an aquaponics PID system
   *//


   import digitalio
   import time
   import board
   import adafruit_hcsr04
   import neopixel
   from PID_CPY import PID             

   print(" hey ")  #this was an earlier test to test if are code was working
   sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D3, echo_pin=board.D2)    #our pins for are ultrasonic sensor
   Kaz = neopixel.NeoPixel(board.NEOPIXEL, 1)   # an homage to kaz who helped on this part of the project  
   KazOutput = 0   # same thing
   relaypin = digitalio.DigitalInOut(board.D8)  # relay pin setup 
   relaypin.direction = digitalio.Direction.OUTPUT # relay pin setup continued 

   pid = PID( 0.5, -0.1, 0, setpoint = 24)    #where we enter our PID and then set our setpoint distance
   PID.output_limits = (0, 1)  # our PID was added, as intened, somewhat later into the construction of our project so we aimed for simplicity 

   while True:
       try:
           Hi = pid(sonar.distance)      
           if Hi == 1 : 
              relaypin.value = True      #where the value effects if the valve is open or not
               print("open")
          else :
              relaypin.value = False    
              print("closed")
          time.sleep(0.1)         #the time our sesnor wait tells it senses again
      except RuntimeError:
           print("Retrying!")   #incase the distance found an error it would print retrying on the montior
      time.sleep(0.1)
~~~

Big thanks to Kaz for helping us figure out how PID code works. 


## Reflection  

A lot of the difficulty of this project was learning each individual piece and then seeing if it would fit with the whole system. For future reference I would; one: make sure the valve we used didn't need a threshold water pressure, two: make sure the valves flow rate can keep up with the pump, three: design the project with PID in mind so that the last week isn't spent trying to intigrate the PID code and four: ultra sonic sensor do work on water. The sulutions to these problems differ from stupid common sense to ignorance of the exact specs of something ordered from amazon, So make sure your output rate can be more than the inlet, intigrate and build around PID code from the start and Plan Plan Plan. oui oui baggette 

   

  


