export CUDACXX=/usr/local/cuda/bin/nvcc
cmake -DCMAKE_INSTALL_PREFIX=/home/computer/workspace/yolo/install/ ../darknet/ .
cmake --build . --target install --parallel 8

export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
./darknet detector demo cfg/coco_my.data cfg/yolov4-tiny.cfg yolov4-tiny.weights 2021-07-30T03-59-28.mp4 -dont_show -ext_output -out_filename aaaaa.avi > 11.txt
