# Opencv
Compile and Install OpenCV-4.1.0 on CENTOS 7 with Python-3.6

Step 1
Install OepnCV 4 dependencies
OS and applications updates

sudo yum update\n
sudo yum upgrade

Step 2
Install developer tools
sudo yum groupinstall "Development Tools" -y\n
sudo yum install cmake gcc gtk2-devel pkgconfig -y

Step 3
Download OpenCV 4.1.0
cd to your folder\n
wget -O opencv-4.1.0.zip https://github.com/opencv/opencv/archive/4.1.0.zip\n
unzip opencv-4.1.0.zip

Step 4
Download OpenCV_Contrib-4.1.0
cd to your folder\n
wget -O opencv_contrib-4.1.0.zip https://github.com/opencv/opencv_contrib/archive/4.1.0.zip\n
unzip opencv_contrib-4.1.0.zip

Step 5
Use virtualenv (More information here: https://realpython.com/python-virtual-environments-a-primer/)
workon cv4

Step 6
Install numpy to virtualenv
pip install numpy

Step 7
Compile and install
Target opencv folder is /usr/local

cd opencv-4.1.0
mkdir build\n
cd build\n
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=~/Documents/opencv_contrib-4.1.0/modules -D BUILD_EXAMPLES=ON ..

Note: Check the cmake output carefully before running make, there should be reference to python3 and numpy. If you need to start over, just delete build folder and recreate it, run cmake again.

make\n
sudo make install

Step 8
Configure softlink in virtualenv to /usr/local/lib/site-packages
cd /usr/local/lib/python3.6/site-packages/cv2/python-3.6\n
ls\n
cv2.cpython-36m-x86_64-linux-gnu.so\n
mv cv2.cpython-36m-x86_64-linux-gnu.so cv2.so\n
cd ~/.virtualenvs/lib/python3.6/site-packages/\n
ln -s /usr/local/lib/python3.6/site-packages/cv2/python-3.6/cv2.so cv2.so

Step 9 
Run simple test

>python
Python 3.6.7 (default, Dec  5 2018, 15:02:05) 
[GCC 4.8.5 20150623 (Red Hat 4.8.5-36)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import cv2\n
>>> cv2.__version__\n
'4.1.0'\n
>>> 

Step 10
Delete opencv-4.1.0.zip and opencv_contrib-4.1.0.zip.\n
Delete opencv-4.1.0 folder.
