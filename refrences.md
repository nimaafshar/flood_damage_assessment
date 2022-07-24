## Dataset

#### Overview of Xview2 Challenge and data

- [XView 2 Challenge | Part 1: Getting Started](https://lezwoncastelino.medium.com/xview-2-challenge-part-1-getting-started-270c2249e19e)

    - definition of [Ground sample distance](https://en.wikipedia.org/wiki/Ground_sample_distance)

- [XView 2 Challenge | Part 2: Setting up Sagemaker](https://lezwoncastelino.medium.com/xview-2-challenge-part-2-setting-up-sagemaker-49090d9167ea)

- [Xivew 2 Dataset MetaData Description](./res/xBD_Metadata_Explanation.pdf)

- [XView 2 Challenge: Part 3: Exploring the Dataset](https://medium.com/analytics-vidhya/xview-2-challenge-part-3-exploring-the-dataset-ec924303b0df)

- [xview2 challenge notebook by *LEZWON CASTELLINO* on kaggle](https://www.kaggle.com/code/lezwon/xview2-challenge/notebook)

- [Xview2 Website](https://xview2.org/download-links)
    - Data has `tier3`, `train` and `test` sets
    - Each set has `images`, `labels` and `targets` folder (`test` has some differences)
    - `tier3` Folder is added to the dataset in the middle of challanges
    - `images` Folder contains *pre-disaster* and *post-disaster* images. filenames are in the format `{disaster-name}_{id}_{pre/post}_disaster.png`
    - **Important Notice**: Some of the post imagary are slightly shifted from their corresponding pre image. also the dataset has different ground sample distances.
    - `labels` folder contains json files containing polygons for each pre/post disaster image. this polygons indicate buildings. in pre disaster images polygons don't have any damage level. but in post disaster images they do. disaster types are `destroyed`, `major-damage`, `minor-damage`, `no-damage`, `un-classified`. the majority of polygons are labeled `no-damage` in post disaster images. so the dataset is highly unbalanced.
    - Distribution of classes in `train` set:
        ```json
        {
            'destroyed': 13227,
            'major-damage': 14161,
            'minor-damage': 14980,
            'no-damage': 117426,
            'un-classified': 2993
        }
        ```
        Distribution of classes in `test` set:
        ```json
        {
            'destroyed': 3775,
            'major-damage': 3850,
            'minor-damage': 4798,
            'no-damage': 41427,
            'un-classified': 1012
        }
        ```

- [Xview2 Challenge Baseline Repository](https://github.com/DIUx-xView/xView2_baseline)
    - Counts `un-classified` damage type as `no-damage`
    - Fine-tunes *Spacenet* to use for localization task.
    - Utilizes *ResNet50* + some colvolutional layers for damage-classification task.
    - The classification task uses the bounding box of polygons + a scaling factor to build input images. then resizes them to $128*128$ and feeds them into the classification network.
    - First stage of each pipeline is to distribute images and label files into different folders based on their disaster. for example:

        `guatemala-volcano_00000000_post_disaster.png` 

        moves to 
        
        `guatemala-volcano/00000000_post_disaster.png`

    - Its a baseline repository so it contains no useful methodology and it's models have low performance.

- [XView2 Challenge First Places Solution Repository](https://github.com/DIUx-xView/xView2_first_place)


## TO READ

- `learn2learn` [repository](https://github.com/learnables/learn2learn) (mentioned techniques)

- [object detection notebook example](https://databricks.com/notebooks/1_data_eng_xview_object_detection.html)
