----------------------------------------------------------------------------------------------------------------
Under …models/research/object_detection/samples/configs copy and move the

“faster_rcnn_inception_v2_pets.config” file into a new folder called training under …models/research/object_detection 

From this link, download the “faster_rcnn_inception_v2_coco” model and extract it twice using 7-zip to obtain a folder called “faster_rcnn_inception_v2_coco_2018_01_28”

Open the config file with notepad and make the following changes: 

Line 9: change the number of classes to number of objects you want to detect (1 in this case)

Line 106: change fine_tune_checkpoint to the path of the model.ckpt.meta file (in “faster_rcnn_inception_v2_coco_2018_01_28” folder)

Line 123: change input_path to the path of the train.records file

Line 135: change input_path to the path of the test.records file

Line 125–137: change label_map_path to the path of the label map

Line 130: change num_example to the number of images in your test folder (1 in this case)


----------------------------------------------------------------------------------------------------------------
In the …\models\research folder (Anaconda prompt):
Run the following commands:

Python setup.py build
Python setup.py install

Open the Slim folder and copy the Nets folder within it

Navigate to C:\Users\<your_username_here>\Anaconda3\envs\tensorflow_env\Lib\site-packages\object_detection-0.1-py3.7.egg and paste the Nets folder in this folder.

----------------------------------------------------------------------------------------------------------------
Navigate to …models/research/object_detection  and run the main.py file in anaconda prompt using the following command: python model_main.py --logtostderr --model_dir=training/ --pipeline_config_path=training/faster_rcnn_inception_v2_pets.config
Training should start after about a couple of minutes and can take 1-2 hours to reach a reasonable loss depending on the data set and the processing speed of the computer
Train until the loss is ~0.05 (should not be too low or model is memorizing data set – overfitting)
Take note of the last saved checkpoint when the training is stopped (check the training folder to see the latest saved checkpoint if anaconda prompt has been quit)
To export the interference graph (so we can run the model), enter the following command (XXXX is latest model checkpoint number): python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-XXXX --output_directory inference_graph


----------------------------------------------------------------------------------------------------------------
