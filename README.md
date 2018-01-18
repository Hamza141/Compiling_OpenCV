# Compiling OpenCV 3.2.0 + OpenCV Contrib

# Step 1: Update all programs

	$ sudo apt-get update
	$ sudo apt-get upgrade
	$ sudo reboot now

# Step 2: Download/Install build tools

	$ sudo apt-get install build-essential cmake pkg-config

# Step 3: Download/Install required libraries

	$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
	$ sudo apt-get install libgtk2.0-dev libgstreamer0.10-0-dbg libgstreamer0.10-0 libgstreamer0.10-dev libv4l-0 libv4l-dev
	$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
	$ sudo apt-get install libxvidcore-dev libx264-dev
	$ sudo apt-get install libatlas-base-dev gfortran
	$ sudo apt-get install default-jdk ant
	$ sudo apt-get install libgtkglext1-dev
	$ sudo apt-get install v4l-utils
	
# Step 4: Download/Install python libraries

#### For python2

	$ sudo apt-get install python-numpy python-scipy python-matplotlib

#### For python3
	
	$ sudo apt-get install python3-numpy python3-scipy python3-matplotlib	


# Step 5: Download/Install pip

	$ wget https://bootstrap.pypa.io/get-pip.py

#### For python2

	$ sudo python get-pip.py
	
#### For python3

	$ sudo python3 get-pip.py
	
# Step 6: Download/Install python-dev

#### For python2

	$ sudo apt-get install python2.7-dev

#### For python3

	$ sudo apt-get install python3-dev
	
# Step 7: Download/Install numpy

#### For python2

	$ sudo pip install numpy

#### For python3

	$ sudo pip3 install numpy
	
# Step 8: Download OpenCV 3.2.0 and OpenCV_Contrib 3.2.0 and unzip them

	$ cd ~
	$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.2.0.zip
	$ unzip opencv.zip
	$ wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.2.0.zip
	$ unzip opencv_contrib.zip

# Step 9: Prepare the build

	$ cd ~/opencv-3.2.0/
	$ mkdir build
	$ cd build
	$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
		-D CMAKE_INSTALL_PREFIX=/usr/local \
		-D INSTALL_C_EXAMPLES=OFF \
		-D INSTALL_PYTHON_EXAMPLES=ON \
		-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.2.0/modules \
		-D BUILD_EXAMPLES=ON \
		-D ENABLE_NEON=ON ..

# Step 10: Compile OpenCV source code

	# Replace 4 with the number of threads your CPU is capable of
	$ sudo make -j4 
	
	# If any errors occur and the process fails to continue, execute
	$ sudo make clean
	
	# Sometimes using multithreading can cause problems, so if you face any problems execute
	$ sudo make
	# Keep in mind that this will take much longer

# Step 11: Install the build prepared in step 9

	$ sudo make install
	$ sudo ldconfig

# Step 12: Edit some files

	$ sudo nano /etc/ld.so.conf.d/opencv.conf

#### Add the following line

	/usr/local/lib          

#### Save opencv.conf by pressing CTRL+O
	
#### Exit to the command line by pressing CTRL+X

	$ sudo ldconfig

	$ sudo nano /etc/bash.bashrc

### Add the following lines at the bottom of bash.bashrc file

	PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig       
	export PKG_CONFIG_PATH

#### Leave an empty line at the end of the file

#### Save bash.bashrc by pressing CTRL+O 

#### Exit to the command line by pressing CTRL+X

# Step 13: Reboot

	$ sudo shutdown -r now

# Step 16 Last Step: Verify OpenCV is installed

#### For example, in python3

	$ python3
	>>> import cv2
	>>> print cv2.__version__
	
#### The output should be
	'3.2.0'