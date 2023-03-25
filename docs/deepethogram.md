### Install deepethogram (GUI)


```
conda create --name deepethogram python=3.7.4
pip install git+https://github.com/shaliulab/deepethogram
pip install git+https://github.com/shaliulab/vidio

```

### Add new data to the FlyBehaviors deepethogram dataset

1. Label a video with deepethogram
2. Save the label in the corresponding folder in `$DEEPETHOGRAM_DATA`.
3. Send the labels to VSC

```
rsync --copy-links --info=progress2 --info=name0  -arvzhR --include "*/" --include "*.csv" --exclude "*" $DEEPETHOGRAM_DATA/./  login:'$DEEPETHOGRAM_DATA'
```

4. Add the new labels to the dataset with dvc

### View the data tracked by dvc

Add data to dvc

This snippet will add to dvc every .mp4 video and yaml/txt files if it has an accompanying label
The prediction file is skipped

```
find DATA -regex .*csv -exec dvc add {} \;
dvc  list -R --dvc-only . DATA/ > labels.txt
while read label; do folder=DATA/$(dirname $label); echo $folder; dvc add $folder/*mp4; dvc add $folder/*yaml; dvc add $folder/*txt; done < labels.txt
```


```
dvc  list -R --dvc-only $DEEPETHOGRAM_PROJECT_PATH DATA
```

### Download cv2 -> local

```
rsync  --copy-links  -arvzhR --include "*/" --include "*.csv" --exclude "*" cv2:/Users/Antonio/FSLLab/Projects/FlyHostel4/deepethogram/flyhostel_data/flyhostel_deepethogram/DATA/./  $DEEPETHOGRAM_DATA
```

### Download vsc -> local

```
rsync  --copy-links  -arvzhR --include "*/" --include "*.csv" --exclude "*" login:/staging/leuven/stg_00115/Data/flyhostel_data/flyhostel_deepethogram/DATA/./  $DEEPETHOGRAM_DATA
```


### Download predictions to local computer

```
rsync  --copy-links  -arvzhR --include "*/" --include "*_output.h5" --exclude "*" cv2:/Users/Antonio/FSLLab/Projects/FlyHostel4/deepethogram/flyhostel_data/flyhostel_deepethogram/DATA/./  $DEEPETHOGRAM_DATA
```

###

Not working

```
find DATA/./ -type f | sed 's:^:/Users/Antonio/FSLLab/Projects/FlyHostel4/deepethogram/flyhostel_data/flyhostel_deepethogram/:' > labels.txt
sed 's/_labels.csv/.mp4/' labels.txt | rev | cut -f 2- -d / | rev > folders.txt
rsync  --copy-links  -arvzhR --files-from folders.txt -e ssh cv2:/ $DEEPETHOGRAM_DATA
```


### Download folder for a specific experiment, chunk and identity to local computer

```
rsync  --copy-links  -arvzhR --include "*/" --include "FlyHostel3_4X_2023-01-25_17-30-00_000155_002/*" --exclude "*" -e ssh login:/staging/leuven/stg_00115/Data/flyhostel_data/flyhostel_deepethogram/DATA/./  $DEEPETHOGRAM_DATA
```