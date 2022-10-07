## Creating Training Dataset: deeplabcut.create_training_dataset(config, num_shuffles=1, Shuffles=None, windows2linux=False, userfeedback=False, trainIndexes=None, testIndexes=None, net_type=None, augmenter_type=None)
Possible augmenter types are: default, imgaug, tensorpack, and deterministic.
Data augmentation is automatically accomplished by DLC, but default values can be overwritten before training. 
Image augmentation is the process of artificially expanding the training set by applying various transformations (rescaling, rotations) to images to make models more robust/accurate. 
Combines labeled datasets from all videos and splits them into training and test datasets. 
Creates train and test subdirectories in dlc-models. 
Downloads ImageNet pre-trained network weights (determine how much influence input has on output). 
To compare multiple networks: deeplabcut.create_training_model_comparison(config, trainindex=0, num_shuffles=1, net_types=['resnet_50'], augmenter_types=['default'], userfeedback=False, windows2linux=False)
 
## Training Network: deeplabcut.train_network(config, shuffle=1, trainingsetindex=0, max_snapshots_to_keep=5, displayiters=None, saveiters=None, maxiters=None, allow_growth=False, gputouse=None, autotune=False, keepdeconvweights=True)
allow_growth=True: dynamically grows the GPU memory region as necessary
Splits dataset into training and testing sets
To continue training from last saved iteration, find latest snapshot in train subdirectory within the dlc-models directory. In the same folder, edit parameter init_weights in pose_cfg.yaml (in train subdirectory) to add the path of the last/best snapshot (w/o filetype ending). 
init_weights: '/content/drive/MyDrive/clock_reading-guillermo-2021-02-15/dlc-models/iteration-0/clock_readingFeb15-trainset95shuffle1/train/snapshot-36800'
“Loading already trained DLC with backbone:…”. If that’s what is printed out, it’s all good; but if you rather read “Loading ImageNet-pretrained…”, then something is incorrect.

## Evaluating Network: deeplabcut.evaluate_network(config, Shuffles=[1], trainingsetindex=0, plotting=None, show_errors=True, comparisonbodyparts='all', gputouse=None, rescale=False)
plotting=True: plots all testing and training frames with manual and predicted labels
Stored in evaluation-results directory
Evaluates network on saved models at different stages of the training network.  
Change snapshotindex parameter in config parameter to ‘all’
Performance is measured by computing mean average euclidean distance (MAE) between manual labels and the ones predicted by DLC. MAE for all pairs and likely pairs (> p-cutoff) is stored as a csv file (helps exclude occluded body parts).

## Analyzing Videos: deeplabcut.analyze_videos(config, videos, videotype='avi', shuffle=1, trainingsetindex=0, gputouse=None, save_as_csv=False, destfolder=None, batchsize=None, cropping=None, get_nframesfrommetadata=True, TFGPUinference=True, dynamic=(False, 0.5, 10))
To analyze all videos in a folder: deeplabcut.analyze_videos('/analysis/project/reaching-task/config.yaml',['/analysis/project/videos'],videotype='.avi')
To analyze multiple videos in a folder: deeplabcut.analyze_videos('/analysis/project/reaching-task/config.yaml',['/analysis/project/videos/reachingvideo1.avi','/analysis/project/videos/reachingvideo2.avi'])
Results are stored as Hierarchical Data Format (HDF), but to save results as an additional csv file: save_as_csv=True

## Labeling Videos: deeplabcut.create_labeled_video(config, videos, videotype='avi', shuffle=1, trainingsetindex=0, filtered=False, save_frames=False, Frames2plot=None, delete=False, displayedbodyparts='all', codec='mp4v', outputframerate=None, destfolder=None, draw_skeleton=False, trailpoints=0, displaycropped=False)
To label all videos in a folder: deeplabcut.create_labeled_video('/analysis/project/reaching-task/config.yaml',['/analysis/project/videos/'],videotype='mp4')
To label multiple videos in a folder: deeplabcut.create_labeled_video('/analysis/project/reaching-task/config.yaml',['/analysis/project/videos/reachingvideo1.avi','/analysis/project/videos/reachingvideo2.avi'])
To analyze new video based on specific snapshot, enter desired index of the checkpoint to the variable snapshotindex in config.yaml.
