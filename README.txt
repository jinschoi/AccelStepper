Fork of Adafruit's fork of AccelStepper with Adafruit motor shield support.

The original version uses integer millisecond step periods, and always resets the next step time to be the current step time plus the step interval. This reduces the potential timing resolution and makes it difficult to ensure that a commanded move will take a certain amount of time.

I have changed it so that setSpeed() and runSpeed() set the *next* step time. If the current time is later than the next step time, then a step is triggered and the next step time is updated by the step interval. This continues in a loop until the next step time is later than the current time, allowing the stepper to catch up if it has fallen behind. The next step time and step interval are stored as floats.

This change makes it possible to coordinate multiple steppers and have them complete their moves in the expected length of time. However, if one stepper is set to move so quickly that the other is starved of steps, the slower stepper will become very jerky. This library should be rewritten to use timer interrupts.

TO INSTALL: Download zip by clicking "DOWNLOADS" in top right corner. Then uncompress folder and rename to AccelStepper. Make sure that folder contains this README. Then copy to sketchfolder/libraries (see also http://www.ladyada.net/library/arduino/libraries.html)
