# HighPrecisionStepperJuggler
a.k.a Octo-Bouncer. Highly precise stepper motor driving with a Teensy 4.0 and custom pulse generating algorithm and PC based image processing with the goal of getting a machine to juggle a ping pong ball.

[Here's](https://electrondust.com/2020/03/01/the-octo-bouncer/) a blog post with more infos about this project. And [here's](https://youtu.be/lYyAMDYzJQM) a YouTube video of the machine in action.

The Arduino folder contains the code for the Teensy 4.0. The Teensy 4.0's job is simple:

- Listen for movement comments on the serial bus
- Generate pulses for the stepper motors

The Unity folder contains the code for the Unity Application. This Application is responsible for:

- Set up the camera (120 FPS 640×480 data stream, gain, exposure, contrast, ISO, saturation) via OpenCV
- Set up Camera Device and getting image stream via OpenCV
- Run Image Processing and get 2D pixel position of ping pong ball
- Get 3D position of ping pong ball using the results of above-mentioned image processing
- Calculate ball velocity
- Use ball position and velocity in PID/Analytical control code to calculate correction-tilt of plate
- Execute Inverse Kinematic code to figure out how much each motor needs to rotate in order to get the plate to a certain height with a     specific tilt.
- Send result of IK calculation to the microcontroller via serial interface
- Render machine position and movements
- Render image processing data
- Render graph showing several data streams

The UVCCameraPlugin folder contains the C++ code for the camera plugin. This is a Unity plugin. All the OpenCV code is being executed in here.

# Important
You need to download openCV 4.2 and get the `opencv_world420.dll` from the build folder and put it inside Plugins/UVC Camera Plugin next to `UVCCameraPlugin.dll`. If you don't do that you'll get below error message on play:

```
Plugins: Failed to load 'Assets/Plugins/UVC Camera Plugin/UVCCameraPlugin.dll' because one or more of its dependencies could not be loaded.
```

Also, you need to use Unity Editor version 2019.2.6f1. It won't run with newer versions.