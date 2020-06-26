//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤Most overkill ignition for 2stroke ever¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤

//Setup
int PinHall = A0;                 //Analog Hall.
int Strobelight1 = 9;             //simple LED strobelight for visualizing spark.

void setup() {
  Serial.begin(921600);
  pinMode(Strobelight1, OUTPUT);

}

//Mechanical setup
int toothtotalcount = 11;         //Example, 11 tooths on wheel + 1 Missing = 11 as value.
float HallDegree = 90;            //Hall mount angle
float FireNormalDegree = 0;       //Normally where spark should fire at TDC.


//FireOffsets
float FireAimDeviation = 2.00;        //+-Degrees of play for the system to find the fire solution when the crank is rotating.
float FireOffset = 0;               //If spark still is offset from desired point, you can add offset here for adjustment.


//SPARKTABLE
bool SparkTableEnable = true;     //Enable or disable sparktable
int SparkTablePrecision = 100;     //Change this value to use 50s 100s 500s or 1000s in the sparktable.
const int SparkTableAmountOfValues = 20; //CHANGE THIS FOR CORRESPONDING OF TOTAL VALUES IN THE TABLE

int SparkTable[SparkTableAmountOfValues][2] = {  
   {0, 0} ,
   {100, 5} ,
   {200, 10} ,
   {300, 15} ,
   {400, 25} ,
   {500, 30} ,
   {600, 35} ,
   {700, 40} ,
   {800, 45} ,
   {900, 50} ,
   {1000, 55} ,
   {1100, 60} ,
   {1200, 65} ,
   {1300, 70} ,
   {1400, 75} ,
   {1500, 80} ,
   {1600, 85} ,
   {1700, 90} ,
   {1800, 95} ,
   {1900, 100}
};


//NUMBERS TO PLAY WITH IF HAVING TROUBLE.
float triggerdelta = 1.2;                       //Previous tooth timings * this ratio for expecting the missing tooth.
int hallsensorgate = 300;                       //Gate value for recognize hall blipps
float CrankNominalRevSpeedsArray[250];          //If you somehow have more than 250 tooths.. O_o






//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤WE ARE FORMED BY TIMESPACE IN MULTIPLE DIMENSIONS¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤

//---------------------------------UTILLITIES-------------------------------------------------

int roundUp(int numToRound, int multiple)
{
    if (multiple == 0)
        return numToRound;

    int remainder = abs(numToRound) % multiple;
    if (remainder == 0)
        return numToRound;

    if (numToRound < 0)
        return -(abs(numToRound) - remainder);
    else
        return numToRound + multiple - remainder;
}

//---------------------------------GLOBAL VARIABLES-------------------------------------------------

//MASTER CLOCK
unsigned long CurrentMicros = 0;

//InputValues
int HallSensorValue;

//Trigger
int trigger = 0;
int triggerlast = 0;


//BLIPP
bool blippreset = false;
bool bloppreset = false;
bool CrankRevolutionClockReset = false;
bool SparkTableLookupReset = false;
unsigned long BlippGlobalTime = 0;
unsigned long BlippTimeGap = 0;
unsigned long blippcounter = 0;
unsigned long MissingBlippDeltaTime = 0;
unsigned long MissingGlobalExpectedTime =0;
unsigned long BlippPrevTriggerGap = 0;

//Missing Tooth
bool missingtoothcheck = false;
int missingtoothdebug = 0;

//Toothcounter
int toothcirclecount = toothtotalcount+1;
unsigned long toothcount;
unsigned long buskeeperLength = 0;

//ToothNominalClockValue
unsigned long ToothNominalClock = 0;

//ToothSmoothClock
float ToothSum = 0;
float CrankRevMicroSeconds = 0;

//CrankRevClock
unsigned long CrankRevClock = 0;
unsigned long CrankRevClockPrev = 0;
unsigned long CrankRevClockGlobal;



//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤

void blipp(unsigned long blippcurrenttime){
  //----Its all about the god damn clock----//
            //----+++++++++++----//
    BlippPrevTriggerGap = BlippTimeGap;
    BlippTimeGap = blippcurrenttime - BlippGlobalTime;
    MissingBlippDeltaTime = (BlippPrevTriggerGap*triggerdelta);
    MissingGlobalExpectedTime = blippcurrenttime + MissingBlippDeltaTime;
    BlippGlobalTime = blippcurrenttime;
  //-------And some other important things to keep in mind----//
    blippcounter++;
    toothcounter(1);
    missingtoothcheck = true;
    missingtoothdebug = 0;
    
}

void MissingToothTest(){
  //I love the future
  if (CurrentMicros > MissingGlobalExpectedTime && missingtoothcheck == true){
    missingtoothcheck = false;
    toothcounter(toothcirclecount);
    missingtoothdebug = 1;
  }
}


void toothcounter(int toothinput){
  //1 == add one
  //ToothCircleCount, i MAX value == maximize and reset
  //Since this guy is triggered by blipp and Missing tooth, keeping count, he will dominate the Nominal clock values..
  //He also gives Nominal Time a favored bus that he thinks always leaves in time.
  
  if (toothinput == toothcirclecount){
    toothcount = toothcirclecount;
    }
  if (toothinput == 1){
    toothcount++;
  }
  if (toothcount >= toothcirclecount+1){
    toothcount = 1;
  }
  if (toothcount == 1){
    //Steady pulse for the Crank Clock
    CrankRevolutionClockReset = true;
    SparkTableLookupReset = true;
    }

  if (toothcount == 3){
    buskeeperLength = BlippTimeGap;
  }
  ToothNominalClockValue(buskeeperLength);

}


void ToothNominalClockValue(unsigned long NominalTimeLength){
  //I am the timekeeper, you all will obey my rules of spacetime, especially the Missing Tooth, i hate busses not leaving in time...
  unsigned long KeeperLength = NominalTimeLength;
  ToothNominalClock = BlippTimeGap;
  if (toothcount == 1){
    ToothNominalClock = KeeperLength;
  }
  
  //I like time so much, i wil make it run smoother with my beloved friend, but i hate him, because he cannot do stuff in realtime.
  ToothSmoothClock(ToothNominalClock);
}


void ToothSmoothClock(unsigned long NominalClock){
  //I love statistics, but it takes time to figure out, so i cannot show the results until something has happend.
  CrankNominalRevSpeedsArray[toothcount] = NominalClock;
  if (toothcount == 1){
    ToothSum = 0;
  for (int i = 1; i < (toothcirclecount+1); i++) {
    ToothSum = ToothSum + CrankNominalRevSpeedsArray[i];
    }
   //MicrosecondsPerTooth
   ToothSum = ToothSum / toothcirclecount;
   //MicrosecondsPerRevolution
   CrankRevMicroSeconds = ToothSum * toothcirclecount;
  }
 }

void CrankRevolutionClock(){
  CrankRevClock = CurrentMicros - CrankRevClockGlobal;
    if (CrankRevolutionClockReset == true){
      CrankRevClock = 0;
      CrankRevClockGlobal = CurrentMicros;
     }
  CrankRevolutionClockReset = false;
}
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤LIGHTSPEED NERD ENDS HERE¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤



//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤GEARHEADS STARTS HERE¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤

//RPM calculation based on one revolution.
float RPM = 0;
  void CrankRPMperRev(float MicrosecondsPerRev){
    //Revolutions per Microseconds to Milliseconds.
    float CrankMillisecondsPerRev = MicrosecondsPerRev/1000;
    //Milliseconds per degree.
    float CrankDegreePerMillisecond = CrankMillisecondsPerRev * 0.001;
    //Revolutions per Second
    float CrankRevPerMillisecond = 1 / CrankDegreePerMillisecond;
    //Revolution per Minute
    RPM = CrankRevPerMillisecond * 60;
    }

//Crank Degree Location Clock.
float CrankDegree = 0;
  void CrankDegreeClock(){
    CrankDegree = (CrankRevClock / CrankRevMicroSeconds)*360;
  }



//Uses Sparktable and rounds RPM to calculate a fire solution
float RPMrounded = 0;
int SparkTableCurrentDegreeOffset = 0;
  void SparkTableLookup(){
    //THIS PROBABLY NEEDS SOME ARRAY FROM PREVIOUS RPMs SO IT DOES NOT MOVE SPARK TOO MUCH.
    
    if (SparkTableEnable == true){
      
      if (SparkTableLookupReset == true){
        SparkTableLookupReset = false;
        
          //RPM Rounded value
          RPMrounded = roundUp((RPM), SparkTablePrecision)-SparkTablePrecision;
          
          //Lookup the degree from sparktable
            for(int i = 0; i < SparkTableAmountOfValues; i++) {
              int lookthru = SparkTable[i][0];
                if (lookthru == RPMrounded){
                  SparkTableCurrentDegreeOffset = SparkTable[i][1];
                   }
             }
      }
    }
  }


//FireOffsets
float FireSolution = 0;
float FireLowerDeviation = 0;
float FireHigherDeviation = 0;

  void FireOffsets(){
      float FireUserOffsets = ((HallDegree + FireOffset)+FireNormalDegree)+SparkTableCurrentDegreeOffset;
      FireSolution = FireUserOffsets;
      
      FireLowerDeviation = FireUserOffsets - FireAimDeviation;
      FireHigherDeviation = FireUserOffsets + FireAimDeviation;
  }


//Switch off the light, and close your eyes, feel the energy inside... chili bo.. chili bo.. chili bo..
//FIREEE!!
float FireTrigger = 0;

void Fire(){
    if(CrankDegree >=FireLowerDeviation && CrankDegree <= FireHigherDeviation){
      Strobelight(1);
      Spark(1);
      FireTrigger = 1;
      }
    else{
      Strobelight(0);
      Spark(0);
      FireTrigger = 0;
      }
}

//Blinky!
void Strobelight(int lightstate){
  digitalWrite(Strobelight1, lightstate);
  }
  
//Sparky!
void Spark(int sparkstate){
}


//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
//¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤

void loop() {
  //-----Master Clock-----//
  CurrentMicros = micros();
  unsigned long ProgramTimeStart = CurrentMicros;     //Used for debugging
  HallSensorValue = analogRead(PinHall);





  //------THIS IS DONE BEFORE THE CLOCKS TO MAKE SURE A FIRESOLUTION IS READY AS SOON AS POSSIBLE-----//
  
  CrankRevolutionClock();
  CrankRPMperRev(CrankRevMicroSeconds);
  CrankDegreeClock();
  SparkTableLookup();
  FireOffsets();
  Fire();



 
  //¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤PiewPiewPiew¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤
 //-----Check for the missing tooth-----//
  MissingToothTest();
  
  //-------HallGate-----//
  //Hall sensor is HIGH
    if (HallSensorValue < hallsensorgate){
     trigger = 1;
    }
    //Hall sensor is LOW
    else{
      trigger = 0;
    }
  //-------BLIPP BLOPP COUNTER-----//
  //---BLIPP---///
  if (trigger != triggerlast) {
    
      if (trigger == HIGH) {
       blipp(CurrentMicros);
        }

       if (trigger == LOW) {
        //BLOPP!
         }
  }
  triggerlast = trigger;
  //---END BLIPP BLOPP COUNTER-----//
  //¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤PiewPiewPiew¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤¤



  DebugWorld();




}







//########################################################################
int debuglevel = 12;
//########################################################################
/* 0 = Off.
 * 1 = Outputs programruntime.
 * 2 = Hallsensor Value
 * 3 = Trigger Value
 * 4 = Tooth Count
 * 5 = BlippTimeGap for every tooth
 * 6 = Missing Tooth trig
 * 7 = BuskeeperLength
 * 8 = Buskeeper vs Blipp vs Nominalclock vs Smooth revolution
 * 9 = Crank Revolution in microseconds
 * 10 = RPM
 * 11 = Crank Degree
 * 12 = RPM Rounded VS RPM
 * 13 = Spark deviation
 * 
 * Serial port Plotter v1.3.0 has been used.
 */



//#########################DEBUG WORLD########################
//You can move these around to check processing time.
//DebugSpecificStart(CurrentMicros);
//DebugSpecificStopPrint(micros());


//""""""""""""""""FUNCTIONS FOR DEBUGGING""""""""""""""""""""

//Debug Processing Clocks
unsigned long DebugSpecificStartTime = 0;
  void DebugSpecificStart(unsigned long CurrentTime){
    DebugSpecificStartTime = CurrentTime;
  }

unsigned long DebugSpecificStopTime = 0;
  void DebugSpecificStopPrint(unsigned long CurrentTime){
    DebugSpecificStopTime=CurrentTime;
      unsigned long DebugTotalTime = DebugSpecificStopTime - DebugSpecificStartTime;
        Serial.print("$");
        Serial.print(DebugTotalTime);
        Serial.print(";");
  }

  void DebugValue(unsigned long inputvalue){
        Serial.print("$");
        Serial.print(inputvalue);
        Serial.print(";");
  }


//#########################################################################################
void DebugWorld(){

  //Hall Sensor Raw input
  if (debuglevel == 2){
    DebugValue(HallSensorValue);
  }
  //Trigger blipp blopps
  if (debuglevel == 3){
    DebugValue(trigger);
  }
  if (debuglevel == 4){
    DebugValue(toothcount);
  }
  if (debuglevel == 5){
    DebugValue(BlippTimeGap);
  }
  if (debuglevel == 6){
    DebugValue(missingtoothdebug);
  }
  if (debuglevel == 7){
    DebugValue(buskeeperLength);
  }
   if (debuglevel == 8){
    Serial.print("$");
    Serial.print(BlippTimeGap);
    Serial.print(" ");
    Serial.print(buskeeperLength);
    Serial.print(" ");
    Serial.print(ToothNominalClock);
    Serial.print(" ");
    Serial.print(ToothSum);
    Serial.print(";");
  }
  if (debuglevel == 9){
    DebugValue(CrankRevMicroSeconds/8);
  }
  if (debuglevel == 10){
    DebugValue(RPM);
  }
  if (debuglevel == 11){
    DebugValue(CrankDegree);
  }
  if (debuglevel == 12){
    Serial.print("$");
    Serial.print(RPMrounded);
    Serial.print(" ");
    Serial.print(RPM);
    Serial.print(";");
  }
   if (debuglevel == 13){
    Serial.print("$");
    Serial.print(FireSolution);
    Serial.print(" ");
    Serial.print(FireLowerDeviation);
    Serial.print(" ");
    Serial.print(FireHigherDeviation);
    Serial.print(";");
  }
  if (debuglevel == 14){
    DebugValue(FireTrigger);
  }








  
}

