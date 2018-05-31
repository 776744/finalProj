# McDonald's Near Me

# Purpose / Description

First, the user is prompted to enter a state and city. The computer will begin by narrowing down the list of possible restaurant locations based on the state the user entered. Then it will find the coordinates of that city and compare it the coordinates of McDonald’s restaurant locations within the state. Which ever restaurant’s coordinates match closest to the coordinates of the city the user entered, that will be labeled as the location closest to the user / the user’s city. The plan is to have the program return at least four more restaurant locations, each one further from the user than the last.

### Difficulties or opportunities you encountered along the way.

The toughest part was not being able to use RegEx because we're not good enough. RegEx would've made this project much easier.

### Most interesting piece of your code and explanation for what it does. --> See further below in code.

```Java
// NOTICE: Program is in Alpha. Still has some bugs.

import processing.sound.*;
import javax.swing.*; 
String city, state, matchfoundTester, ccString, title, statelabel, citylabel, coordlabel, closestlocationslabel, c1, ccX, ccY, ccX2, ccY2, closestLocation, closeloc2, closeloc3, closeloc4, closeloc5;
String[] cities, restrcord, splitIt;
int indexFinder, charFinder1, charFinder2;
double ccIntX, ccIntY, ccIntX2, ccIntY2;

void settings(){
  size(750,450);
}

void setup()
{
  background(0);
  noStroke();
  frameRate(60);
  fill(255,255,0);
  cities = loadStrings("latlng.txt");
  restrcord = loadStrings("mcdonalds.txt");
  c1="*";
  title="McDonald's Near Me";
  statelabel="State :: ";
  citylabel="City :: ";
  coordlabel= "City Coordinates :: ";
  closestlocationslabel="Five Close Locations:";
  try { 
    UIManager.setLookAndFeel(UIManager.getSystemLookAndFeelClassName());
  } 
  catch (Exception e) { 
    e.printStackTrace();
  } 
  String enterstate="State Initials";
  String entercity="City";
  state = JOptionPane.showInputDialog(frame, "Enter your state's initials:", enterstate);
  city = JOptionPane.showInputDialog(frame, "Enter the name of your city:", entercity);
}

void draw()
{
  background(0);
  frameRate(60);
  while(matchfoundTester!=city){
    for(int i=1; i<cities.length-1; i++){
      if(city.equalsIgnoreCase(cities[i].substring(10,10+city.length())) && state.equalsIgnoreCase(cities[i].substring(36,36+state.length()))){
          indexFinder = i;
          matchfoundTester=city;
          ccString=cities[indexFinder].substring(39,42)+"."+cities[indexFinder].substring(43,49)+", "+cities[indexFinder].substring(49,53)+"."+cities[indexFinder].substring(54,59);
          ccX=cities[indexFinder].substring(40,48);
          ccY=cities[indexFinder].substring(50,59);
      }
    }
  }
  textSize(26);
  text(title,225,50);
  textSize(14);
  text(statelabel,25,125);
  text(c1,390,150);
  text(c1,390,180);
  text(c1,390,210);
  text(c1,390,240);
  text(c1,390,270);
  text(citylabel,25,200);
  text(coordlabel,25,275);
  text(closestlocationslabel,375,120); 
  text(city.substring(0,1).toUpperCase()+city.substring(1).toLowerCase(),70,200);
  text(state.toUpperCase(),75,125);
  text(ccString,155,275);
  ccIntX = Double.parseDouble(ccX)/1000000;
  ccIntY = Double.parseDouble(ccY)/1000000;
  
  //double[] xVals = new double[restrcord.length];   DOESN'T WORK
  //double[] yVals = new double[restrcord.length];   DOESN'T WORK
  
  
//### Most interesting piece of your code and explanation for what it does.

// This scans specifically for the coordinates in the mcdonalds.txt file. It finds the coordinates, which at the time are strings. Then it parses those strings into doubles to be used to compare with the coordinates found in the latlng.txt file. 
  for(int i=0; i<restrcord.length; i++){
     charFinder1=restrcord[i].indexOf(',');
     charFinder2=restrcord[i].indexOf('"');
     ccY2=restrcord[i].substring(1,charFinder1);
     ccX2=restrcord[i].substring(1+charFinder1,charFinder2-1);
     ccIntX2=Double.parseDouble(ccX2);
     ccIntY2=Double.parseDouble(ccY2);
     
   /**  DOESN'T WORK
     xVals[i] = ccIntX2;
     yVals[i] = ccIntY2;
     if((Math.abs(ccIntX-xVals[0])<Math.abs(ccIntX-xVals[i])) && (Math.abs(ccIntY-yVals[0])<Math.abs(ccIntY-yVals[i]))){
       splitIt=restrcord[i].split(",",5);
       closestLocation=splitIt[4];
     }
   */  
    
     if(Math.abs(ccIntX-ccIntX2)<=.1 && Math.abs(ccIntY-ccIntY2)<=.1){
       splitIt=restrcord[i].split(",",5);
       closestLocation=splitIt[4];
     }
     if((Math.abs(ccIntX-ccIntX2)<=.15 && Math.abs(ccIntY-ccIntY2)<=.15)){
       splitIt=restrcord[i].split(",",5);
       closeloc2=splitIt[4];
     }
     if((Math.abs(ccIntX-ccIntX2)<=.25 && Math.abs(ccIntY-ccIntY2)<=.25) || (Math.abs(ccIntX-ccIntX2)<=.3 && Math.abs(ccIntY-ccIntY2)<=.3)){
       splitIt=restrcord[i].split(",",5);
       closeloc3=splitIt[4];
     }
     if((Math.abs(ccIntX-ccIntX2)<=.35 && Math.abs(ccIntY-ccIntY2)<=.35) || (Math.abs(ccIntX-ccIntX2)<=.4 && Math.abs(ccIntY-ccIntY2)<=.4)){
       splitIt=restrcord[i].split(",",5);
       closeloc4=splitIt[4];
     }
     if((Math.abs(ccIntX-ccIntX2)<=.45 && Math.abs(ccIntY-ccIntY2)<=.45) || (Math.abs(ccIntX-ccIntX2)<=5 && Math.abs(ccIntY-ccIntY2)<=5)){
       splitIt=restrcord[i].split(",",5);
       closeloc5=splitIt[4];
     }
  }
  textSize(12);
  text(closestLocation,400,150);
  
  /** DOESN'T WORK
   text((int)xVals[0],480,350);
   text((int)xVals[1],480,360);
   text((int)xVals[2],480,370);
   text((int)xVals[3],480,380);
  */
  
  text(closeloc2,400,180);
  text(closeloc3,400,210);
  text(closeloc4,400,240);
  text(closeloc5,400,270);
}

```
## Built With

* [Processing](https://processing.org/) - The IDE used

## Authors

* Jason Thoennes & Kofi Owusu


## Acknowledgments

* Thanks to Dr. R for providing all sorts of data sets for us to use.
