# Ar-Ding-Nition
# 2 stroke Arduino ignition - Missing tooth trigger wheel ignition.
This project is halted.


Before reading:
- This is my first project written on the Arduino.
- I have no prior experience of C++ or ignition systems.
- Unfinished, still tons of things left to do in the code.
- Stopped the project at problems with the board freezing at random. But engine running ok at lower RPM.

Purpose of the project:
- Low cost.
- 2 Stroke Tuning.
- Simple configuration.
- Homebrew with parts laying around.
- Minimal effort with the capability to have a sparktable.

Requirments:
- Arduino IDE 1.8.13. (Problems running code on lower)
- Serial Port Plotter v.1.3.0. (For debugging)
- Hall Sensor. (Honeywell gt101dc were used during development with pulldown resistor)
- Trigger wheel with 1x missing tooth. (11 tooths +1 missing were used)
- Mosfet
- Spark coil

This code looks for the missing tooth, calculating the crank degree. Looks up a sparktable and fire the desire signal when i position.


