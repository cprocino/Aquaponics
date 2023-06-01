# Robot Arm


* [Intro](#intro)
* [Planning](#planning)
* [Visuals](#visuals)
* [Code](#code)
* [Wiring](#wiring)
* [Reflection](#reflection)

---


## intro
This project was based around the idea of PID and our task was to build a system using PID to keep one variable in the system constant. We decided to do a aquaponics system with the controlled variable being the water level of the plant tank. Our system would be relatively simple, the entire system would be essentially enclosed inside a large 20 gallon fish tank. The tank would be partially filled with water that would act as a reservoir their would then be a smaller water tank inside that would have its water level controlled via a pump and valve using PID.



## planning 
our planning was rather simple as the construction of our project was largely already made. The below picture is our initial very rough sketch of the basis of our project, it will make much more sense once one views the completed project. The sketch is faithful to our final project with the exception of the monitored tank being suspended instead of laying on some wood on the bottom 



<img src="https://github.com/cprocino/Aquaponics/assets/71406784/925c8a53-bd52-4210-a16a-6adc7ba785c8" height="250">

our planning was slightly skewed by our knowledge of our lack of knowledge in PID 
for the first week after we desided on our project we would create the skeleton of our project using the fish tank and a few other household and lab idems.
the rest of the time we would spend trying to figure out how we would PID the project and how the new valves and pumps could be controlled with arduinos. 








## visuals
<img src="https://github.com/cprocino/Aquaponics/assets/71406784/86a0e908-96a6-4de7-9fcf-735391fd2e29" height="300">

This is a partial picture of our wiring that shows the most important parts ( see wiring diagram for full wiring) 

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/e2a363ca-2033-448c-b5bb-e4b3e986a802" height="300">

This is the board we cut out in order fo make this a viable system for Hydro/aquaponics, it allows us to suspend potatos in the water and lets them grow. 

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/a56aafc4-da36-4c78-8105-d22c0ad17798" height="300">

This is a picture of our small monitiered tank and the valve we used to affect flow.

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/99353b00-bdc5-4b77-abb7-96275dfcf8e0" height="250">

this is the tank that encloses the whole system

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/e11dadc4-419e-4fe5-b15d-2721fd8b6252" height="250">

this is our final pump, the one we first used was to strong and the valve could not keep up with the flow

<img src="https://github.com/cprocino/Aquaponics/assets/71406784/ceef106a-32a8-4821-ae7c-09107d3ca763" height="250">

this is the whole project assembled with out the water or plants. 

## wiring 


  

## code
For our code we had two renditions, one was a simplistic non-PID version that kindof worked it is as follows:



the other was the PID that was in our final version it is as follows:




## reflection  

This project was interesting in that no single part of it was extremely difficult but we needed to learn many different systems before we could complete the project; There was the Pumps that we needed pair with the right valves so that we could properly create the final flow system, the PID code that we need to familiarize ourselves with and the ultrasonic sensors that we were told didn't work on water(they do). A lot of the difficulty of this project was learing each individual piece and then seeing if it would fit with the whole system. 

   

  
