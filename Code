// Include files for required libraries
#include <stdio.h>

#include "opencv_aee.hpp"
#include "main.hpp"     // You can use this file for declaring defined values and functions

void setup(void)
{
    /// Setup camera won't work if you don't have a compatible webcam
    //setupCamera(320, 240);  // Enable the camera for OpenCV
}

int main( int argc, char** argv )
{
    setup();    // Call a setup function to prepare IO and devices

    cv::namedWindow("Photo");   // Create a GUI window called photo
    cv::namedWindow("HSV");
    cv::namedWindow("GREEN");
    cv::namedWindow("RED");
    cv::namedWindow("BLUE");

    while(1)    // Main loop to perform image processing
    {
        Mat frame;
        Mat HSV;
        Mat GREEN;
        Mat RED;
        Mat BLUE;
        Mat eroded;

        // Can't capture frames without a camera attached. Use static images instead
        while(frame.empty())
        {
            /// Can't capture frames without a camera attached. Use static images instead
            //frame = captureFrame(); // Capture a frame from the camera and store in a new matrix variable
            frame = readImage("image.bmp");
        }


        cv::imshow("Photo", frame); //Display the image in the window

        cvtColor(frame, HSV, COLOR_BGR2HSV);

        Mat spotFilter = cv::getStructuringElement(MORPH_ELLIPSE, Size(5,5));
        cv::erode(HSV, eroded, spotFilter);

        cv::imshow("HSV", eroded);

        inRange(eroded,Scalar(40, 68, 57), Scalar(73, 255, 255), GREEN);
        int greenNonZero = 0;
        greenNonZero = countNonZero(GREEN);
        cv::imshow("GREEN", GREEN);

        inRange(eroded,Scalar(0, 100, 100), Scalar(10, 255, 255), RED);
        int redNonZero = 0;
        redNonZero = countNonZero(RED);
        cv::imshow("RED", RED);

        inRange(eroded,Scalar(78, 158, 124), Scalar(138, 255, 255), BLUE);
        int blueNonZero = 0;
        blueNonZero = countNonZero(BLUE);
        cv::imshow("BLUE", BLUE);

        if ((greenNonZero > redNonZero) && (greenNonZero > blueNonZero)){
            printf("\nThe object is green");
        }
        else if ((redNonZero > greenNonZero) && (redNonZero > blueNonZero)){
            printf("\nThe object is red");
        }
        else if ((blueNonZero > redNonZero) && (blueNonZero > greenNonZero)){
            printf("\nThe object is blue");
        }

        int key = cv::waitKey(1);   // Wait 1ms for a keypress (required to update windows)

        key = (key==255) ? -1 : key;    // Check if the ESC key has been pressed
        if (key == 27)
            break;
	}

	closeCV();  // Disable the camera and close any windows

	return 0;
}



