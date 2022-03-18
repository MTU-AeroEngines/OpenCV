
# Adding OpenCV to Visual Studio

This page explains how to install and set up OpenCV in Visual Studio 2019, for C++ development.

OpenCV (Open Source Computer Vision Library: http://opencv.org) is an open-source library that includes several hundreds of computer vision algorithms.

## Download and Install OpenCV

1. Download OpenCV, the latest stable release for Windows platform. Go to the official OpenCV website: https://opencv.org/ -> Library -> Releases and click on the Windows platform.
2. Extract OpenCV in the **C directory** of your PC.

## Set up Environment Variable

1. Go to Advanced System Settings -> Environment Variables.
2. Now, under the System Variables section select Path and click on Edit.
3. Click on New and enter the path of the bin folder inside the OpenCV package. The path should be something like this (depending on your installation location) ```:C:\opencv\build\x64\vc15\bin```.
4. Press OK and exit the environment variable window clicking OK.

## Configure Visual Studio Project

1. Open Visual Studio. Click on Create a new project -> Console App -> Type project name -> Create.
2. Once the project created, change the solution platform from x86 to x64 as the debug environment.
3. Now, click on Project -> Properties and go to the Configuration Properties -> VC++ Directories. Under General section:
    - paste path of include folder of OpenCV to ***Include Directories***. The path will be similar to ```C:\opencv\build\include```.   
    - paste the internal path to ***Library Directories*** The path will look similar to ```C:\opencv\build\x64\vc15\lib```.
4. Next, go to linker -> Input and enter the name of the library file that ends with ‘d’ in front of ***Additional Dependencies***. You will find the DLL (Dynamic Link Library) here: ```C:\opencv\build\x64\vc15\lib```, copy the name of the file, similar to ```opencv_world341d.lib```. Then, click Apply.
5. Exit Project Properties by clicking OK.

## Test the code

Now to try this out, download this little test source code or get it from the sample code folder of the OpenCV sources. Add this to your project and build it. 

In the code we open OpenCV logo (https://github.com/opencv/opencv/blob/4.x/samples/data/opencv-logo.png). Before starting up the application, make sure you place the image file in your current working directory. 

```c++
#include <opencv2/core.hpp>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>
#include <iostream>
using namespace cv;
using namespace std;
int main(int argc, char** argv)
{
    if(argc != 2)
    {
     cout <<" Usage: " << argv[0] << " ImageToLoadAndDisplay" << endl;
     return -1;
    }
    Mat image;
    image = imread(argv[1], IMREAD_COLOR); // Read the file
    if(image.empty()) // Check for invalid input
    {
        cout << "Could not open or find the image" << std::endl ;
        return -1;
    }
    namedWindow("Display window", WINDOW_AUTOSIZE); // Create a window for display.
    imshow("Display window", image); // Show our image inside it.
    waitKey(0); // Wait for a keystroke in the window
    return 0;
}
```

![OpenCV logo](https://raw.githubusercontent.com/opencv/opencv/4.x/samples/data/opencv-logo.png)
