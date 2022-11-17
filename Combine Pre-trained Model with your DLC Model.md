### 1. 
Update iteration number in config.yaml. If you do not create a new iteration, init_weights in pose_cfg.yaml will be overwritten to the previous path. In other words, init_weights will not be changed to the specific snapshot you set it to if you are in the same iteration as the previous training session.
### 2. 
Change model type to resnet_101 in config.yaml and pose_cfg.yaml in the train subdirectory. 
### 3. 
Change init_weights in pose_cfg.yaml in the train subdirectory to the path of the latest snapshot from the pretrained model. The path should exclude the extension of the snapshot. 
### 4. 
Create a new training set with resnet_101 by running deeplabcut.create_training_dataset. 
### 5. 
Run deeplabcut.train_network with parameter keepdeconvweights=False. Make sure the path to init_weights is printed to be the path of the snapshot you set it to. 
