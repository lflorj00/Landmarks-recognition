# Landmarks-recognition


To download the oxford datased go to the data foldar and use the following comands:

    wget http://www.robots.ox.ac.uk/~vgg/data/oxbuildings/oxbuild_images.tgz
    mkdir oxford5k_images oxford5k_features
    tar -xvzf oxbuild_images.tgz -C oxford5k_images/
    

Then go to the parameters folder where you need to downoald the pretained models to detect landmarks and extract features:

    wget http://storage.googleapis.com/delf/delf_gld_20190411.tar.gz    --  To extract features
    tar -xvzf delf_gld_20190411.tar.gz
    
    wget http://storage.googleapis.com/delf/d2r_frcnn_20190411.tar.gz   -- For landmark detection
    tar -xvzf d2r_frcnn_20190411.tar.gz
