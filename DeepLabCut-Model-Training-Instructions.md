# DeepLabCut Model Training Instructions

**This guide is for using DeepLabCut in a Jupyter Notebook.**

## Step 1
Select one or more videos to train a DeepLabCut (DLC) model on. Training on a fewer number of frames (about 20 frames) from various videos results in better performance than training on a large number of frames from a single video. About 100 to 200 frames in total give decent results. In addition, instead of using lengthy videos to train a model, trimming videos to about 1 to 2 minutes with the most interesting behaviors is preferred so frames with these interesting behaviors are extracted for manual annotations. 

## Step 2
Edit video file path variable with the path of the video you want to train the model on when creating a new project. This variable may contain a single path or a list of paths if using multiple videos to train the model. To train the model on additional videos, video paths can be added later, whenever needed, using deeplabcut.add_new_videos.
If using Windows, paths must be entered in the following manner:            r'C:\Users\computername\Videos\reachingvideo1.avi' or
'C:\\Users\\computername\\Videos\\reachingvideo1.avi'

## Step 3
Creating a new project creates a config file. In addition, edit config file path variable with the path of the config file in Jupyter notebook. In the config file, edit the list of bodyparts you want to track and modify the skeleton accordingly. If the project folder is moved, the user must remember to update the project_path parameter in the config file (the video paths do not need to be manipulated as they have been copied into the project folder). 

## Step 4
Once the project has been created and the video path(s) have been specified, the user can extract frames from the video(s). Before running deeplabcut.extract_frames, specify the number of frames to be extracted from each video in the config file. After running the cell containing the command deeplabcut.extract_frames, the user is asked if they want to extract frames from each video. The first time running this command, the user should answer yes to each question to extract frames from each video. If the user decides to not use a particular video for training the model, the user should then answer no to the question for that particular video. If the command deeplabcut.extract_frames is being run a second time, the user is asked if they want to add additional frames to the existing frames in the subdirectory in labeled-data. If the user answers yes to this, the number of additional frames is the same as the numframes2pick parameter in the config file. If you do not want to add the same number of frames that were extracted from the video the first time, you must update the number of frames to be extracted in the config file and then run deeplabcut.extract_frames to this new number of frames to the existing frames. 

## Step 5
Once frames have been extracted from the video(s), deeplabcut.label_frames is run and an interactive graphical user interface (GUI) appears. Sometimes this window does not pop up, so the user should check the taskbar. This GUI is used to manually annotate all the frames. Using the Load Frames button, the user needs to select the directory containing the frames that the user wants to annotate. Right click to add a label and click the scroll wheel to remove a label. Left click and drag an annotation to move it to a different position. Use the scroll wheel for removal cautiously as removal of an annotation cannot be undone. If a bodypart cannot be observed clearly in a frame, it is best not to label it. Once all the bodyparts in a frame have been labeled, the user should select the Next Frame button to load the next frame. Once all the frames from a video have been annotated, the user should save the annotations by using the Save button. If more than one video is being used for training, after the frames extracted from one video have been annotated and saved, the user needs to select the Load Frames button again and select another directory that contains frames that have not been annotated yet. 

## Step 6
The cell containing the command deeplabcut.label_frames does not resolve even after the GUI has been closed. The user needs to halt and close the Jupyter notebook and reopen it to resume working.

## Step 7
Once all extracted frames have been annotated, the user can check if the labels were created and stored appropriately using deeplabcut.check_labels. After running this command, each video directory in the labeled data directory should have a subdirectory that contains the word labeled as a suffix. The directories created by this command should consist of frames plotted with the annotated body parts. 

## Step 8
Once the extracted frames have been labeled appropriately, the user needs to run the deeplabcut.create_training_dataset command to split the labeled datasets into training and test sets. The training set is used to train the network while the test set is used to evaluate the trained network. 

## Step 9
To train the network, the user needs to run the command deeplabcut.train_network. This cell does not resolve; it must be interrupted. About 200k training iterations should be allowed before this cell is interrupted or look for when the loss begins to plateau and then interrupt. If the user wants to resume training from a specific checkpoint, they can set the parameter init_weights in the pose_cfg.yaml file in the train subdirectory as the path of the checkpoint from which the user wants to resume training.

## Step 10
To evaluate the network, the user needs to run the command deeplabcut.evaluate_network. The results from evaluating the network are stored in a new direcotry called evaluation-results. 
During the evaluation stage, DO NOT change the paths of the videos in the config file; the video paths should remain the same.

## Step 11
To use the trained network for labeling novel videos, the command deeplabcut.analyze_videos is used. The path of the novel video is passed in as an argument to this command, so once again the video paths in the config file should NOT be manipulated. This command stores the labels for the novel video in a Hierarchical Data Formal (HDF) in the directory where the novel video is stored. 

## Step 12
The labeled novel video using the HDF that has the labels is created by running the command deeplabcut.create_labeled_video. The labeled novel video is stored in the same directory as the original novel video. 

## Step 13
The trajectories of the extracted poses can be plotted using the command deeplabcut.plot_trajectories. 
