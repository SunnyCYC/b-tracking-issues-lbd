# What Can Go Wrong When Conducting Beat Tracking Experiments

This is the repo for the ISMIR late-breaking demo paper titled
"*What Can Go Wrong When Conducting Beat Tracking Experiments*".

## Abstract
Automated beat tracking is a central task in music information retrieval (MIR) and aims to find time positions that humans would tap along when listening to music. In a previous contribution [1], we built upon an existing beat tracking system and evaluated the results on annotated datasets of Western classical music. In our experiments, we obtained poor evaluation results which we first attributed to the complexity of the music. We later discovered that many of the poor results can be traced back to technical issues in the processing pipeline and inaccurate beat annotations. In this contribution, we report on some of these issues and make suggestions regarding visualization and sonification to better understand the data and results.

## Technical Issues of madmom library [2]
To reproduce the technical issues of madmom libraray, we provided one 30-second audio clip of one track from ASAP[3] and the converted three formats of the same track (see Bach_Fugue_bwv_848_LeeSH01M_30 in the [audio folder](https://github.com/SunnyCYC/b-tracking-issues-lbd/tree/main/audio)). The notebook, [2023-11-02_technical-issue-final.ipynb](https://github.com/SunnyCYC/b-tracking-issues-lbd/blob/main/2023-11-02_technical-issue-final.ipynb), demonstrate the codes to reproduce the artifacts and the figure in our paper.

## Annotation Issues in ASAP dataset [3]
As mentioned in our paper, there are three types of issues found in the ASAP dataset, including shifted beat anntoations, missing beat annotations, and unreasonably short inter-beat intervals (IBIs). While there are intuitive methods to detect these issues, further visualization, sonification, and inspection are required to confirm if it is indeed an annotation error. In this repo, we provide the csv files for tracks with potential annotation issues. And provide the visualization and sonification methods in the .ipynb notebooks.

### Missing Beat Annotations
Missing beat annotations can be detected by IBIs longer than a threshold (e.g., 10 seconds), or the audio duration after the last beat annotation. For example, if a track with audio duration much longer than the final beat annotation, there are likely to be missing annotations. We found two tracks in ASAP with abnormal duration after the final beat annotations:


| Track name | Duration after the last beat (second) |
| -------- | -------- |
| Beethoven_Piano_Sonatas_9-1_Tysman05M   | 170.08    |
| Beethoven_Piano_Sonatas_11-1_MaximovI02M   | 1009.56     |


### Unreasonably Short Inter-Beat Intervals
[annotation-statistics.csv](https://github.com/SunnyCYC/b-tracking-issues-lbd/blob/main/annotation-statistics.csv) shows the IBI statistics of all tracks in ASAP. The unit of tempo related terms (e.g., min_max_temporange, mean_tempo, min_tempo, max_tempo) are all in BPM. One may find several tracks with max_tempo over 1000 BPM. These abnormal IBIs may happen only a few times in a track, which makes it hard to detect. [2023-11-02_abnormal-annotations-final.ipynb](https://github.com/SunnyCYC/b-tracking-issues-lbd/blob/main/2023-11-02_abnormal-annotations-final.ipynb) we demonstrate visualization[4] and sonification methods to detect and inspect these abnormal IBIs. Note that due to the file size limit, the IPython playback function is turned off in the script.

### Shifted Beat Annotations
[org-songlevel-annshift.csv](https://github.com/SunnyCYC/b-tracking-issues-lbd/blob/main/org-songlevel-annshift.csv) demonstrates the F1-score improvenments/changes corresponding to annotation shift (from +/- 2 second, with 10ms hop size) the beat annotations. As mentioned in the paper, tracks with large F1-score improvement are like to have shifted annotations. In [2023-11-03_shifted-annotations-final.ipynb](https://github.com/SunnyCYC/b-tracking-issues-lbd/blob/main/2023-11-03_shifted-annotations-final.ipynb), we demonstrate how to inspect these tracks with visualization[4] and sonification methods.




## Reference
[1] C. Chiu, M. Muller, M. E. P. Davies, A. W. Su, and Y. Yang, “Local periodicity-based beat tracking for expressive classical piano music,” IEEE/ACM Transactions on Audio, Speech, and Language Processing, vol. 31, pp. 2824–2835, 2023

[2] S. Böck, F. Korzeniowski, J. Schlüter, F. Krebs, and G.Widmer, “madmom: A new Python audio and music signal processing library,” in Proceedings of the ACM International Conference on Multimedia (ACM-MM), pp. 1174–1178.

[3] F. Foscarin, A. McLeod, P. Rigaux, F. Jacquemard, and M. Sakai, “ASAP: a dataset of aligned scores and performances for piano transcription,” in Proceedings of the International Society for Music Information Retrieval Conference (ISMIR), 2020, pp. 534–541.

[4] C. Chiu, M. Müller, M. E. P. Davies, A. W. Su and Y. Yang, "An Analysis Method for Metric-Level Switching in Beat Tracking," in IEEE Signal Processing Letters, vol. 29, pp. 2153-2157, 2022.

