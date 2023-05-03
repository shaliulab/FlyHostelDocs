# Running a flyhostel experiment

Flyhostel experiments run on a Petri dish filled with agar and sucrose.
The Petri dish is enclosed by a glass dome of 4 cm in diameter, coated with [SigmaCote](https://export.vwr.com/store/product/26984927/sigmacote-siliconizing-reagent). Sigmacote keeps the animals from walking on the glass in an upside down position, which makes crossings more difficult and restrains animal behavior to an upside up position.  See [document](assets/sigmacote.pdf) for more details on this substance.


## Petri dish preparation

1. Pour 50 ml of deionized water in a bottle and weigh 5 % agar and 5 % sucrose (2.5 grams of each)
2. Pour 200 ml of deionized water in a bottle and weigh 5% agar (10 grams)
3. Autoclave both
4. Pour 25 ml of the agar-only liquified bubble-free mix into Petri dishes (should be enough for 7-8).
5. Quickly check no bubbles have been formed. Pay special attention to small bubbles that are only visible when looking carefully
6. Place the [mould for the food patch](assets/foodPatchMould.stl)
7. Once the agar is solidified, remove the mould and pour with a 1000 ul pipette the mix that contains sucrose. Load at least 500 and gently pour until the hole is filled and no more. A small bulge is OK and actually recommended because flat food patches tend to detach from the surrounding sugar-free agar, ruining the experiment

## Sigmacote glass preparation

1. Make sure the glass is clean by applying ethanol 70% and gently rubbing it with fiber-free paper.
2. Remove excess ethanol with deionized water and leave to dry in an oven at 50 deg C. 
3. Pour 50 ml of sigmacote with a pipette in the inner side of the glass i.e. the side facing the flies
4. Gently turn the glass around to ensure the product covers most of the surface
5. Leave again to completely dry in the same oven at 50 deg C.
6. Dip a couple of times in deionized water to clean any debris from the sigmacote.
7. Leave to dry for a third and last time in the same oven at 50 deg C.

## Incubation of Petri dish + glass

1. Leave the filled Petri dish with its glas in the incubator for at least an hour to make sure it reaches temperature and humidity balance with the new environment.
-> This helps prevent the formation of water droplets at the onset of the experiment, which can have fatal consequences for the animals. They can drawn inside the droplets, or get their wings stuck to the glass due to excess humidity, which also kills tehm

2. Take this opportunity to check the appearance of the Petri dish with the camera, to detect any particles of dust or cotton that could have been depositeed on the glass or agar while loading it in the incubator, and clean it if necessary with a paintbrush.

3. Take this opportunity to check the appearance of the Petri dish with the camera, to detect any irregularities on its surface that may indicate lower quality. Some markers to look out for:

    * Irregular attachment between the food patch and the rest of the agar
    * Wave like patterns on the agar
    * Significant bubbles that were somehow missed in the previous checks


## Load flies

1. Prepare a big bucket with ice
2. Make sure enough water is present in the humidifier.
3. Make sure the sensor works by querying it from the recording computer by running `curl sensor:9000`
3. Prepare the [fly loader](assets/flyLoader.stl) by filling all its slots with eppendorf PCR tubes
4. Prepare a locomotor tube with a sealed end.
5. Blow one fly at a time from the vials and place in the locomotor tube
6. Gently shake the tube so the fly falls inside one eppendorf tube. The locomotor tube has a slightly smaller diameter than the eppendorf tube, which makes it relatively easier to get the fly in it. Quickly close the eppendorf tube, while being careful not to crush the fly
6. Get one Petri dish from the incubator and remove any excess humidity accumulated on the glass with a fiber-free paper and gloves.
7. Once all flies have been poured in isolated eppendorf tubes, put in the ice and wait a few seconds until all flies pass out. Should not take longer than 30 seconds, unless a fly keeps crawling at the top of the eppendorf tube, which may have less contact with ice. Shake the tube in that case, to make sure the fly falls to the bottom, which is in contact with the ice
8. Once all flies have passed out, open the eppendorf tubes and pour all the animals onto the Petri dish. Try to place them around the food patch but not on it, to avoid a potential crush with the glass (because the food is slightly higher). Place the glass as quickly as possible
9. Put the Petri dish back in the incubator and start the experiment using the CLI explained in [camera](camera.md)