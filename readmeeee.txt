значит если юзать системный opencv из пакета стандартного, то opencv будет юзать gstreamer бэкенд и будет читать файлы с фреймрейтом видео файла, это нам не подходит, нам надо быстро все фреймы читать.
Для этого надо собрать opencv с ffmpeg бэкендом и сказать darknet'у его юзать:

sudo dnf install gtk3-devel gtk2-devel ffmpeg-devel
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/home/computer/workspace/opencv_for_darknet_install -D INSTALL_PYTHON_EXAMPLES=OFF -D INSTALL_C_EXAMPLES=OFF -D OPENCV_ENABLE_NONFREE=ON -D WITH_FFMPEG=ON -D WITH_GSTREAMER=OFF -D ENABLE_FAST_MATH=1 -D HAVE_opencv_python3=OFF -D BUILD_EXAMPLES=OFF ../opencv .
cmake --build . --target install --parallel 8

всё, если opencv версия новая будет не 4.5.3, то правим еще CMakeLists.txt в darknet, исправляем версию. Без версии cmake стандартный opencv находит почему-то.
С ffmpeg бэком 4-минутное видео обрабатывается за секунд 10 наверно, в отличии от gstreamer а в котором 4 минутное видео будет 4 минуты и обрабатываться.

 

export CUDACXX=/usr/local/cuda/bin/nvcc
cmake -DCMAKE_INSTALL_PREFIX=/home/computer/workspace/yolo/install/ ../darknet/ .
cmake --build . --target install --parallel 8

export LD_LIBRARY_PATH=/home/computer/workspace/opencv_for_darknet_install/lib64:/usr/local/cuda/lib64:$LD_LIBRARY_PATH
./darknet detector demo cfg/coco_my.data cfg/yolov4-tiny.cfg yolov4-tiny.weights 2021-07-30T03-59-28.mp4 -dont_show -ext_output -out_filename aaaaa.avi > 11.txt
