# Agrobot
A fully automated robot which can perform all of the tasks except harvesting on an agricultural field  

  So, this was our final year B.Tech project regarding the use of AI and ML in it (Since we were from the AI&DS department)  
  There isn't much to explain on how to launch the program/robot,  
  Anyway, I'll be explaining how the robot works.  

  The robot uses an arduino Mega2560 R3 + WiFi board and we've hard coded each module representing each function the robot can perform on the field.  
  The data flow within the total system is as follows :  
   ![Flowchart](https://github.com/sagar-s-abraham/Agrobot/blob/main/Images/DFD%202.png?raw=true)  
   For easier understanding, the left side contains the input modules where the sensors and the camera percieves data from the field,  
   The middle blocks contain the UI for the farmer to interact with the robot and the microcontroller within the arduino board, and also 2 ML models which are hosted in the computer system.  
   The right side contains the actuator modules which perform certain functions on the field based off of the decisions taken by the controller.  

   So, The robot is connected over WiFi and the user can command it over the Blynk app in mobile, the robot uses a normal UltraSonic system to traverse through the field in a straight line, and acts according to 
   the command its given.  
   
   If the command is for  
   Seeding : the seeder attachment which was made using a 3D printer is fixed onto the robot and it will travel through the field at a slow pace so that each spoke of the seeder firmly places a minimum of 2 seeds 
   at a time.  
   
   Irrigation : The robot stops at different spots throughout the field and reads the soil moisture level of the ground. If its below a preset threshold, the water pump activates until the soil moisture reading rises.  
   
   Humidity & Temperature : The DHT sensor placed on the robot reads the current temperature and humidity levels of the field and sends this data over WiFi to the Blynk app which then informs the user if any action is needed.  
   
   Classification : The robot uses OV7670 cameras and stops when the plant is in front of it. After taking a snapshot, the image is sent over WiFi and given as input to a YOLOv8 model which has been trained to differ between crops and weeds.  
   If the model classifies it as 'Weed', the weeder actuator which includes 2 blades made using a 3D printer is rotated at an angle so that it uproots the weeds from the ground.  
   If the model Classifies it as 'Crop', the program control is given to the detection model.  
     
  Detection : After the plant is classifed as a crop, the robot moves a little bit forward until the crop is under the pesticide spraying module. 
   Consider the crop within a circle and divide it into 8 sectors. We've used a special attachment (which was also made using the 3D printer) which has 2 arms that are diametrically opposite. Both of these arms are equipped with a camera and a floodjet nozzle. The attachment rotates using a servo motor and both cameras take pictures of the 8 sectors by only turning 4 times. These images are then sent over WiFi to a CNN model which scans the images to find areas of infection/disease on the crop. The sectors which have disease are noted and the attachment rotates to it so as to spray the plant with the pesticide.

   
