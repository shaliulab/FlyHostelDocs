To add examples to the FlyFinder dataset:


### Find imperfect frames

Choose a good collection of "imperfect" frames. These are frames that idtrackerai has flagged as problematic and are saved in `basedir/idtrackerai/imperfect` in the VSC

### Download from VSC

in cv2, run

```
conda activate yolov7
load2fiftyone --dataset FlyFinder --frames-folder http://localhost:8001/basedir/idtrackerai/imperfect/frames --labels-folder http://localhost:8001/basedir/idtrackerai/imperfect/yolov7/labels --count NUMBER_OF_ANIMALS --n-jobs 1 --class-id 0
```

if `--n-jobs` > 1, the samples are donwloaded in parallel
`--class-id` set to 0 means only detections of the class 0 will count for the match against the number of animals

This will download the samples from the VSC and add them to the fiftyone dataset with the predictions produced by YOLOv7 included.


### Annotate using CVAT

in cv2, run


```
conda activate yolov7
fiftyone-dataset --dataset FlyFinder
# for example
KEY="FlyHostel1_2X_2023-02-08_13-20-00"
view=dataset.match(F("tags").contains(KEY))
view.annotate(ANN_KEY, label_schema={"ground_truth": {"type": "detections"}, "prediction": {"type":  "detections"}}, url="http://10.43.205.5:8081")
```

This will upload the samples to cvat for human annotation. To download the annotations at any time back to fiftyone (even if not all samples are annotated)

```
view.load_annotations(ANN_KEY)
```


Note: cvat can be accesed via http://10.43.205.5:8081/ thanks to the following configurations, which are already implemented and are left here for documentation purposes
i.e. they don't have to be repeated every time, only once.

`/Users/Antonio/FSLLab/Projects/YOLOv7/cvat/docker-compose.yml`

```
    ports:
      - 8080:8080
```
for
```
    ports:
      - 8081:8080
```

`~/.bashrc`

```
export CVAT_HOST=10.43.205.5
export FIFTYONE_CVAT_USERNAME=vibflysleep
export FIFTYONE_CVAT_PASSWORD=flysleep1
```