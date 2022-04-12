from dataclasses import dataclass


Quantification
=====================

The quantification of behavior is a complex topic, and many algorithms and approaches can be taken to extract different types of information from the data.


## Sleep amount

#### Single point modelling

idtracker.ai returns the X, Y coordinate of the center of each fly over time, keeping track of their identities. We can use this, together with some heuristics that define sleep (lack of locomotor activity for more than 5 minutes) to quantify sleep in the fly hostel.

Analysis should be done using the `XXXXXX.npy` trajectory files produced by copying the idtracker.ai output. See (idtrackerai)[idtrackerai.md]





