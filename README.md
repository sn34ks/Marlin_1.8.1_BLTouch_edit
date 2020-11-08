# Marlin_1.8.1_BLTouch_edit
This Git contains the firmware and mounting bracket for upgrading a Lulzbot TAZ 6 to use a BL Touch for Bed leveling

Currently my bed on my TAZ 6 has been upgraded to a magnetic PEI coated steel bed (Like Prusa MK3S).  I do not have the washers on the four corners of the bed so I don't have to worry about the nozzle hitting the washers.  

** IMPORTANT - if you use this firmware as it sits, the nozzle will crash into a washer.  You will need to modify the BLTouch safe probe area in the Conditionals_LulzBot.h so that the nozzle does not crash into the washer.  These lines of code start at #444

#elif defined(LULZBOT_USE_AUTOLEVELING) && defined(LULZBOT_TAZ_BED)   //BLTouch probe area
    #define LULZBOT_LEFT_PROBE_BED_POSITION       60 // Starting Point with Washers & Default Bed
    #define LULZBOT_RIGHT_PROBE_BED_POSITION     300 // Starting Point with Washers & Default Bed
    #define LULZBOT_BACK_PROBE_BED_POSITION      245 // Starting Point with Washers & Default Bed
    #define LULZBOT_FRONT_PROBE_BED_POSITION      30 // Starting Point with Washers & Default Bed
#endif

** PROBE MOUNTING - If you use a different probe than the one in this git, you will need to change these values to reflect the position of the probe in relation to the nozzle.  Behind and to the right of the nozzle is a positive number.  In front of and to the right of the nozzle is a negative number.  This is also in the Conditionals_LulzBot.h starting at line# 506

   +-- BACK ---+
   |           |
 L |    (+) P  | R <-- probe (20,20)
 E |           | I
 F | (-) N (+) | G <-- nozzle (10,10)
 T |           | H
   |    (-)    | T
   |           |
   O-- FRONT --+
 (0,0)

#define LULZBOT_MULTIPLE_PROBING              2
#define LULZBOT_X_PROBE_OFFSET_FROM_EXTRUDER  23    //BLTouch offset from nozzle NAR
#define LULZBOT_Y_PROBE_OFFSET_FROM_EXTRUDER  73
#define LULZBOT_Z_PROBE_OFFSET_RANGE_MIN      -2
#define LULZBOT_Z_PROBE_OFFSET_RANGE_MAX      5
#define LULZBOT_XY_PROBE_SPEED                8000

** MESH GRID - Lulzbot TAZ 6 uses only 4 points to level the bed by default.  You can change this to as many as you want in the marlin code.  For example, I have found 4x4 to work the best for me which is actually 16 points.  The BLTouch will take 16 points of reference instead of the original 4.  Play with this and see which works best for you.  This is also in the Conditionals_LulzBot.h starting at line# 471

  #define LULZBOT_GRID_MAX_POINTS_X            4    //BLTouch grid points
  #define LULZBOT_GRID_MAX_POINTS_Y            4
  #if defined(LULZBOT_IS_MINI)
