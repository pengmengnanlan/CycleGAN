# CycleGAN
 style transfer of unpaired images based on CycleGAN


## Resource
https://github.com/junyanz/CycleGAN

## Enviornment
tensorflow-gpu,cuda,cudnn

## Main steps
* data preprocessing：collect datasets(man2woman dataset from celeA), use `build_data.py` to turn .jpg into .tfrecords which is required by tensorflow.

     --X_input_dir datasets/a_resized
     
     --Y_input_dir datasets/b_resized

     --X_output_file datasets/man.tfrecords

     --Y_output_file datasets/woman.tfrecords

* data training: use `train.py` to train (parameter: input dirs, img size)
     
     --X datasets/man.tfrecords

     --Y datasets/woman.tfrecords
     
     --image_size 256


* check: use tensorboard (trained data will be stored in ./checkpoints)

     --logdir checkpoints/20200303-2243 
     

* model generating from trained data: use `export_graph.py` (parameter: dirs of trained data you want to use, X_Y_model, Y_X_model). It will generate two models: from X to Y and from Y to X

    --checkpoint_dir checkpoints/20200303-2243

    --XtoY_model man_to_woman.pb

    --YtoX_model woman_to_man.pb

* model testing: use `inference.py` to test model (parameter: the model you want to use, input dirs, output dirs)

    --model pretrained/man_to_woman.pb

    --input data/input.jpg

    --output data/output.jpg
    
* continue to train after interruption: use `train.py`

    --load_model 20180819-23467

## Result
* trained model by codes: ./pretrained/man_to_woman.pb, ./pretrained/woman_to_man.pb
* test results of trained model after 16h, 19h, 31h can be checked in ./test/manwoman
* models downloaded from CycleGAN: ./pretrained/apple2orange.pb, orange2apple.pb, zebra2horse.pb, horse2zebra.pb
* test results can be checked in ./test/orangeapple and ./test/zebrahorse
* you can download models(.pb) to test directly
