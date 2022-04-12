idtrackerai.ai
=======================

We use idtracker.ai to segment and track multiple individuals in the same arena


Once a recording has been completed, you can analyze with idtrackerai, like this:

## Set analysis params in the GUI

1. Open the imgstore with idtrackerai

![open_idtrackerai](assets/idtrackerai_gui.png)

2. Required input:

* Number of animals
* Area thresholds
* Intensity thresholds
* Session name (datetime)
* Apply ellipse ROI. Provide 5 interspaced points along the outer outline of the glass dome

-> Save parameters with name _datetime_.conf

3. Open the _datetime_.conf file and remove

1. Session name
2. Video name
3. Chunk number


## Schedule chunk analysis

```
cd $ROOT_OF_VIDEOS_FOLDER

idtrackerai-loop --input `pwd`/./2022-03-11_22-41-00_ROI_0 --interval 0 5 --knowledge-transfer previous --environment idtrackerai4 --suffix "" --jobs 15
```

* `--jobs` sets the maximum number of CPU cores to use. Please set it to a conservative value, depending on your total number of CPUs and the other processes which may be running in your PC.

* `--interval` determines which chunks of your store will be analyzed. The second number is the first chunk which is NOT analyzed (i.e. as in range(0, 5), which means 0 1 2 3 4, and not 5)

* `--input` must receive a path to a folder with an imgstore. The path should be split with `/./`, to indicate what is the root, and what is the imgstore folder itself. Everything after the dot will be hardcoded into the data, which still allows to move the imgstore around without the idtrackerai results breaking.

* `--environment` should contain the name of a anaconda environment which contains the required software
* `----knowledge-transfer` set to previous if knowledge transfer from the previous chunk should be used
* `--suffix` if the name of the imgstore contains anything after the datetime. Otherwise, just pass the empty string

# idtrackerai repository version
62391f982531f3b8ab665d5f753bda169ed9dada


# task spooler
https://github.com/justanhduc/task-spooler
https://github.com/justanhduc/task-spooler/releases/tag/v1.3.0


# rsync
```
# from the videos folder
rsync -arvz  -R --include "*/" --include "metadata.yaml" --include "*conf" --exclude "*" ./EXPERIMENT_FOLDER/ cv1:/Users/Data/flyhostel_data/videos/
rsync -arvz  -R --include "*/" --include "*mp4" --include "*npz" --include "*json" --include "*png"  --exclude "*" ./EXPERIMENT_FOLDER/ cv1:/Users/Data/flyhostel_data/videos/
```
# Analyse trajectories

The coordinates for every chunk are stored in the `trajectories.npy` file under 

`EXPERIMENT_FOLDER/idtrackerai/session_XXXXXX/trajectories/trajectories.npy`

The entrypoint `fh-copy` will copy the `trajectories.npy` of each session to `XXXXXX.npy` on the EXPERIMENT_FOLDER, this way, besides the .json, .npz, .mp4 and .png files, a .npy becomes available for every chunk. The resulting copy should never be edited. Instead, one should edit them with python video annotator and copy the edited file in `EXPERIMENT_FOLDER/idtrackerai/session_XXXXXX/trajectories/trajectories.npy` back to the `EXPERIMENT_FOLDER`.

For example, from the videos folder:

```
fh-copy --imgstore-folder 2022-04-02_16-09-56 --analysis-folder 2022-04-02_16-09-56/idtrackerai/
```
will perform the `EXPERIMENT_FOLDER/idtrackerai/session_XXXXXX/trajectories/trajectories.npy` -> `EXPERIMENT_FOLDER/XXXXXX.npy` copies
