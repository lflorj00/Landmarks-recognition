# Landmarks-recognition

To install all the dependencies follow this instructions:

    https://github.com/tensorflow/models/blob/master/research/delf/INSTALL_INSTRUCTIONS.md


To download the oxford dataset go to the /data folder and use the following comands:

    wget http://www.robots.ox.ac.uk/~vgg/data/oxbuildings/oxbuild_images.tgz
    mkdir oxford5k_images oxford5k_features
    tar -xvzf oxbuild_images.tgz -C oxford5k_images/
    

Then go to the /parameters folder where you need to downoald the pretained models to detect landmarks and extract features:

    wget http://storage.googleapis.com/delf/delf_gld_20190411.tar.gz    --  To extract features
    tar -xvzf delf_gld_20190411.tar.gz
    
    wget http://storage.googleapis.com/delf/d2r_frcnn_20190411.tar.gz   -- For landmark detection
    tar -xvzf d2r_frcnn_20190411.tar.gz

Once you download all the dependencies you can try how the extraction and the detection works:

Steps to landmark detection:
    
   1. Include the images in list_images_detector.txt
    
    echo data/oxford5k_images/all_souls_000002.jpg >> list_images_detector.txt
    echo data/oxford5k_images/all_souls_000035.jpg >> list_images_detector.txt
    
   2.Download the model in the /parameters folder.
    
   3.Detect the landmark using this command:
    
    python3 extract_boxes.py \
        --detector_path parameters/d2r_frcnn_20190411 \
        --detector_thresh 0.8 \
        --list_images_path list_images_detector.txt \
        --output_dir data/oxford5k_boxes \
        --output_viz_dir data/oxford5k_boxes_viz
        
  
Steps to extracts and matching features:

   1.Download the oxford dataset in the /data folder.
   
   2.Include the two images tho extract features and compare them:
   
    echo data/oxford5k_images/hertford_000056.jpg >> list_images.txt
    echo data/oxford5k_images/oxford_000317.jpg >> list_images.txt
    
   3.Download the model in the /parameters folder
   
   4.Using this command it will extract the features of the images include in list_images.txt:
   
    python3 extract_features.py \
        --config_path delf_config_example.pbtxt \
        --list_images_path list_images.txt \
        --output_dir data/oxford5k_features
    
   5.The next command will compare the features from both images and save the results in form of an image:
   
    python3 match_images.py \
        --image_1_path data/oxford5k_images/hertford_000056.jpg \
        --image_2_path data/oxford5k_images/oxford_000317.jpg \
        --features_1_path data/oxford5k_features/hertford_000056.delf \
        --features_2_path data/oxford5k_features/oxford_000317.delf \
        --output_image matched_images.png
   
   
   
