Backup
=================


flyhostel creates big data. In order to safely maintain it, we use Dropbox on Ubuntu

The flyhostel video recordings are saved to a folder monitored by the Dropbox client for Linux, which automatically saves to the remote Dropbox cloud server. The high resolution videos take < 50 MB / 5 minutes. However, the idtrackerai temporary folders (inside `idtrackerai/`) take 5.5 GB / 5 minutes for videos of 6 flies and < 1 GB for single fly videos. This poses a challenge to store and especially to analyze videos across different computers.

In order to send video data to another system, we use rsync. See [idtrackerai](idtrackerai.md)

In order to exchange files between Dropbox and a computer (both ways) using a CLI, we use [dropy](https://github.com/shaliulab/dropy)

The last validated hash of the dropy project:

```
6fc78004c9186fc3a667065e08943d93f6fe71bc
```


In order to manually UPload a folder in the local computer to Dropbox

```
# verify the token is valid
> cat /etc/dropy.conf
{"token": "sl.BCDNydSVaN4vv0xGnfO2P8_uwcRSIAiYkbkwsgwd1VRce_zB1j2CaLFSwRUKyT6fgvkmsYQVWC6Z-5aFNRx_ftbMV2ncqOPNB2o1g83J3JxYTWubVwTzrY0BWlXBv39_k9dr4J2t"}

```

```
# start the CLI version of Dropbox (if dropy-init has not been run yet)
> dropy-init
```

```
# upload the desired folder to Dropbox
> dropy /Users/Data/flyhostel_data/videos/EXPERIMENT_FOLDER/idtrackerai/./session_XXXXXX Dropbox:/Data/flyhostel_data/videos/EXPERIMENT_FOLDER/idtrackerai/
```

```
#for many folders, say session_000000 to session_000200
START=1
END=200

for SESSION in $(seq -f "%06g" START END);
do
    SRC="/Users/Data/flyhostel_data/videos/EXPERIMENT_FOLDER/idtrackerai/./session_${SESSION}"
    DEST="Dropbox:/Data/flyhostel_data/videos/EXPERIMENT_FOLDER/idtrackerai/" # ending in / is essential
    echo "Copying ${SRC} -> ${DEST}" 
    dropy ${SRC} ${DEST};
done
```

In order to DOWNload the Dropbox folder in the remote to the local computer


Option 1) Enable it in the Dropbox client GUI and the client will download it in the background

Option 2) Manually download it by spawning a Dropy process again


```
# start the CLI version of Dropbox (if dropy-init has not been run yet)
> dropy-init
```

```
# download the desired folder from Dropbox
> dropy  Dropbox:/Data/flyhostel_data/videos/${EXPERIMENT_FOLDER}/idtrackerai/session_${SESSION} `pwd`/session_${SESSION} --recursive
```




