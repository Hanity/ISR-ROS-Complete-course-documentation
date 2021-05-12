# ISR-ROS-Complete-course-documentation
#  Intelligence and Smart Robotics : Robot Operating System


#The Robot Operating System (ROS) is a set of software libraries and tools that help you build robot applications. From drivers to state-of-the-art algorithms, and with powerful developer tools, ROS has what you need for your next robotics project. And it's all open source
please visit: http://wiki.ros.org/ for more detailed information


This folder contains documentation for a ISR course taught in Leeds Beckett University.The course is taught by Dr.  Abiodun Yusuf. 

The pdfs in this repository are the tasks and projects done in this course so the solution to the problem is stated below

The folder structure is as follows :

#   ROS Noetic Installation
For this course, we have used the latest ROS Noetic Ninjemys Ubuntu 20.04. These ROS distribution released in May 23rd, 2020. There are other version of ROS but ROS Noetic was chosen because it supposts python 3 and others support python 2 which is now depricated.

 
For installation, please  follow the steps provided in the following link: http://wiki.ros.org/noetic/Installation/Ubuntu


# Detailed lecture was taught by Dr.  Abiodun Yusuf from creating work space to detailed deployment of codes.

   ## Before writing and running codes the following procedures were done:


  ###  Creating  a workspace
  We have created a folder called **catkin_ws** which represents our workspace. catkin was designed to be more conventional than rosbuild, allowing for better distribution of packages, better cross-compiling support, and better portability.Within this folder we manually created the **src** folder then we used the command 
  
  `catkin_make`. This created the **build** and **devel** directories.
  
  #*# (side note...This created a lot of problem when running at the beginning hence uninstalling it and installing again is easier than trying ti find other solution I found it to be time consuming.)
  
  ### Creating the my_robot_tutorial package
  This package is created inside **catkin_ws/src/** using the command `catkin_create_pkg my_robot_tutorial roscpp rospy std_msgs`

  ### Launching roscore
  The first thing that needs to be done when using ROS is to always run ROSCORE command in terminal. done everytime we use ROS. This command launches the ROS Master which is the central node for all other ROS nodes that communicate to build a full ROS-based system. Only one instance of this can be called.
  
  **Note**
  Each time a new terminal is opened, we have to source our workspace using the command `source devel/setup.bash`
#   ROS Nodes
A ROS node can be considered the basic unit of ROS Packages.Nodes are exuctable files they can either be python codes, C++ codes standard messages and so on.They are excecutable files. The node uses a ROS cient library to communicate with other nodes through a publish-subscribe relationshipp.For the purpose of this course the nodes are created within the scripts located in the directory `catkin_ws/src/my_robot_tutorial/scripts/`



The first example node created is a python code labelled as  **my_first_node.py**. Followed by the same codes only written in C++


#   Publishers/Subcribers
These are common ideas and the names actually explain the functionality. Basically publishers are codes that send messages under a specified topic. Subscribers are codes that search to receive the messages sent under the topic they look for. So one sends and the othe receives.

  #*# (Unrelated information : Publish and subscribe are used in a lot of application such as microcontrollers, Internet of things and so on...)
  
  
  
 ##  Functional Example
In the location `catkin_ws/src/my_robot_tutorial/scripts/` we find the python script `publisher.py` that contains the code to publish the string “Hello care to meet a Robot..lol” under the topic hello_world. Our Subscriber script is in the same folder under the name `subscriber.py`. This last subscribes to the topic Hello care to meet a Robot..lol in order to receive all messages directed to this topic.

The execution of this is as follows:
- Launching the ROS master with the command `roscore`
- In a separate terminal, we run the publisher script using `python3 publisher.py`.
- We confirm that our publisher is working well by using the command `rostopic list`. This displays the topics being published. If we want to see the contents of the messages sent, we use the command `rostopic echo /hello_world`.

- In a separate terminal again, we run the subscriber script using `python3 subscriber.py`. This was done inorder to insure that messages taht are being sent are being receiived correctly .





 ##  Mini-Project Example 1
######  Task given 
The task is creating 2 nodes, the first publishes a value (rpm), and the second subscribes to the value of rpm and publishes the calculated speed.
The detailed description of this mini project can be found in the pdf named `ROS - Pub-Sub-Mini-Project`

   ######  Codes
   The codes for this project are within the files **rpm-pub.py** and **rpm-sub-pub.py**.
   
#   ROS Parameter Server
It is essentially a centralised space to store variables often used and generally linked to robots' physical attributes. 
As the value  change with time such server make it convenient to store them and call the scripts when ever needed.

- **To change** a variable within the parameter server, we use for example the command `rosparam set /wheel_radius 0.155`.
- **To display** a variable within a terminal, we use `rosparam get /wheel_radius`.
- **To call** a variable within our scripts, we use `rospy.get_param('/wheel_size')`.

#   ROS Launch Files
These are files are used  to set variable values in the parameter server and also to launch multiple scripts within a ROS application.This largely simplfies the execution of our codes as it's done in one go instead of the tedious work of manually launching each file in a different terminal.

  ##  Mini-Project Example 2 
  ##### Task given 
  In this mini-project, the task given is to  create a launch file that will execute all the steps required in the previous Pub-Sub mini-project. It will do the following: 
  - Starting the ROS Master.
  - Setting the wheel_radius parameter in the ROS parameter server.
  - Running the RPM publisher.
  - Running the file subscribing to RPM, calculating and publishing the Speed.

  The code is called `speed_cal_sim.launch` and can be found in the directory `catkin_ws/src/my_robot_tutorial/Launch/`
  To execute the code, we use the command `roslaunch my_robot_tutorial speed_cal_sim.launch`
  
  **Keep in mind :** Don't forget to source the workspace whenever you use a new terminal, using `source catkin_ws/devel/setup.bash`

#   ROS Bag Files
A ROS Bag is essentially a device for recording and playing messages that are sent under a certain subject when requested. 
- A Bag file can be launched using the command `rosbag record -a -O test.bag`
- The recorded file can be played in a loop (-l) using the command `rosbag play -l test.bag`

#   ROS Packages
  Software in ROS is organized in packages. They allow us to simplify robot application .Application are broken up in to reusable blocks so as to update and debugging.
   
### Creating packages
Creating a package in ROS is simple and is done using the command `catkin_create_pkg package_name dependencies`
### Installing and using packages
follow the following steps to install packages.
- Follow https://index.ros.org/packages/page/1/time/ and find the suitable package(s) to create your desired application.
- To install a package, use the command `sudo apt install ros-noetic-package_name`
- To use a package, use the command `rosrun package_name file_to_execute`. Note that in most cases the files to execute would be launch files. Also, to achieve your desired result you logically have to run your packages files in the right succession.

#   ROS Services
(ROS.org :The publish / subscribe model is a very flexible communication paradigm, but its many-to-many one-way transport is not appropriate for RPC request / reply interactions, which are often required in a distributed system. Request / reply is done via a Service, which is defined by a pair of messages: one for the request and one for the reply. A providing ROS node offers a service under a string name, and a client calls the service by sending the request message and awaiting the reply. Client libraries usually present this interaction to the programmer as if it were a remote procedure call.
Services are defined using srv files, which are compiled into source code by a ROS client library. )

ROS Services are used to achieve the request-reply (client-server) interaction. So the service received a request from a client, then does the necessary computations and eventually gives a response to the client. Unlike ROS packages, the services are scarce, which means developpers have to create their own services.
The next two examples will be used to demonstrate the creation and usage of services. 

  ##  Functional Example 1: Odd Even Service
 The purpose is to create a simple service that tells the client if the number he sent is odd or even.
  
  - We create the service file named  **OddEvenCheck.srv** and specify the type of input msg to receive from clients and the type of output msg to answer said clients. This is done as follows:
```
int32 number

---

string answer
```

- In the file **package.xml**, we uncomment the following lines:
```
<build_depend>message_generation</build_depend>
<exec_depend>message_runtime</exec_depend>
```

- We edit the **CMakeLists.txt** file as follows:
```
add_service_files(
    FILES
    OddEvenCheck.srv
 )
    
 generate_messages(
   DEPENDENCIES
   sensor_msgs
   std_msgs
 )
 ```
 - We run catkin_make from the catkin workspace root directory.
 - We create the service script called **odd_even_service.py**.
 - Now we can use our created service through a terminal by using the command `rosservice call \OddEvenCheck input` and we will receive an answer.
 - We can also create the client script called **odd_even_client.py** that calls our service and may use it for further things.
 
 **Keep in Mind:**
 All these files are available in the **scripts** folder.


  ##  Project 1: Image Retrieval
  The project is aimed at more advanced approach in  showing the usage of services. The purpose is a service that receives a desired camera angle from the client meaning that angle will be selected.It then turns to the camera to this angle, takes a picture and sends the image back to the client. 
 Therefore to simplify because read me files are also supposed to be to the point ..lol, a folder containing images in angles -30°, -15°, 0°, 15° and 30° is provided. So the service received the desired angle and returns the appropriate image from this folder.
For further details, please consult the pdf named **ROS-Services-Project-Brief**.
The steps are similar to the previous example.
- First, in the **srv** folder, we create the service file **TurnCamera.srv** containing the following:
```
float32 turn_degrees
---
sensor_msgs/Image image
```
- Second, we edit the **CMakeLists.txt** file as follows:
```
## Generate services in the 'srv' folder
add_service_files(
    FILES
    OddEvenCheck.srv
    TurnCamera.srv
 )

## Generate added messages and services with any dependencies listed here
 generate_messages(
   DEPENDENCIES
   sensor_msgs
   std_msgs
   geometry_msgs
 )
```
- Third, we run catkin_make from the catkin workspace root directory.
- Next, we create our service script called **turn_camera_service.py**.
- Lastly, we create our client script called **turn_camera_client.py**

#   ROS Actions
Actions are essentially a service extension.
While in many cases, services are useful in ROS applications, it nevertheless takes a long time for us to run applications.The client would generally want feedback from the service for a period of time, or to be able to stop its performance.The package actionlib contains an action server and an action client. 

The definition of three parameters is:
Goal, feedback and Result 
For more information, please see http://wiki.ros.org/actionlib/.

The second project will showcase Action
  ##  Project 2: 
The description of the project is found in the pdf named **ROS ACTIONS PROJECT BRIEF**
To create this project, we follow the next steps:
- Create a folder named **action** within our **my_robot_tutorial** folder.
- Inside this new folder, we create the file **navigate2D.action** that contains the definition of our 3 parameters:
```
#Goal
geometry_msgs/Point point
---
#Result
float32 elapsed_time
---
#feedback
float32 distance_to_point

```
- We add the following dependencies in the **package.xml** file:
```
<build_depend>actionlib</build_depend>
<build_depend>actionlib_msgs</build_depend>
<exec_depend>actionlib</exec_depend>
<exec_depend>actionlib_msgs</exec_depend>
```
- We edit the **CMakeLists.txt** file as follows:
```
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
  sensor_msgs
  geometry_msgs
  genmsg
  actionlib
  actionlib_msgs
)

## Generate actions in the 'action' folder
  add_action_files(
  FILES
  navigate2D.action
    )

## Generate added messages and services with any dependencies listed here
 generate_messages(
   DEPENDENCIES
   sensor_msgs
   std_msgs
   geometry_msgs
   actionlib_msgs
 )

```
- We run catkin_make from the catkin workspace root directory.
- We create our **action_server.py** script and run it with the command `rosrun my_robot_tutorial action_server.py`
- Create the script **robot_point_pub.py** that sends the current point information to the **action_server.py** script
- We create our **action_client.py** script and run it.

# Important Notes
- Make sure that all python files in the scripts folder are executable using the command `chmod +x *.py`
- Whenever using a new terminal, make sure to source using the command `source devel/setup.bash`
