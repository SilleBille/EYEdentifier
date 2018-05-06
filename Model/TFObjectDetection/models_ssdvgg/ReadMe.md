# SSD-VGG

Instructions:
-------------

1. Download and install the Tensorflow object Detection API by following the instructions on https://github.com/tensorflow/models/tree/master/research/object_detection.
2. Add the VGG feature extractor file(ssd_vgg_feature_extractor.py) to the directory `models/research/object_detection/models`. 
3. Replace the `object_detection/builders/model_builder.py` with the provided model_builder.py.
4. Replace the `object_detection/builders/model_builder_test.py` with the provided model_builder_test.py.
5. Execute `python object_detection/builders/model_builder_test.py` to ensure that new feature extractor is intgerated succesfully.

Dataset:
--------

* Under the directory named 'data', download the pascal VOC dataset using the following commands:

    wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
    tar -xvf VOCtrainval_11-May-2012.tar
    python object_detection/dataset_tools/create_pascal_tf_record.py \
        --label_map_path=object_detection/data/pascal_label_map.pbtxt \
        --data_dir=VOCdevkit --year=VOC2012 --set=train \
        --output_path=pascal_train.record
    python object_detection/dataset_tools/create_pascal_tf_record.py \
        --label_map_path=object_detection/data/pascal_label_map.pbtxt \
        --data_dir=VOCdevkit --year=VOC2012 --set=val \
        --output_path=pascal_val.record

* Under the directory named `checkpoint`, download the VGG 16 classification checkpoint from TF Slim.
* The config file is provided, change the paths accordingly.
* Model can be trained using the command:

        python object_detection/train.py \
            --logtostderr \
            --pipeline_config_path=${PATH_TO_YOUR_PIPELINE_CONFIG} \
            --train_dir=${PATH_TO_TRAIN_DIR}

* Model can be evaluated using the command:

        python object_detection/eval.py \
            --logtostderr \
            --pipeline_config_path=${PATH_TO_YOUR_PIPELINE_CONFIG} \
            --checkpoint_dir=${PATH_TO_TRAIN_DIR} \
            --eval_dir=${PATH_TO_EVAL_DIR}


The train dir and eval dir are both empty directories at the start, found inside `models_ssd_vgg/models`. (the test.txt is an empty file, kept to be able to have empty directories in repo)
