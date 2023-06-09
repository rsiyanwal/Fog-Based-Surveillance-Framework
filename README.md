# Fog-Based-Surveillance-Framework
This IoT architecture utilizes energy-efficient and low-latency devices to monitor a specific area. It leverages ESP-NOW, MQTT, and Apache Kafka communication protocols to enable activity detection and monitoring. The architecture demonstrates the practical application of fog-based IoT architectures. It comprises multiple modules that work together, as shown in the flow diagram below.

<figure>
  <img src="https://user-images.githubusercontent.com/11557572/236662442-a0a3636d-1f54-4770-b4f7-4e3bce6edbaa.jpg" width="72%">
  <figcaption>Flow Diagram of Fog-based Surveillance Framwork; by Rahul Siyanwal</figcaption>
</figure>


## Framework

### Preprequisites
1. Get familier with [Apache Kafka](https://github.com/rsiyanwal/Apache-Kafka-Basics), [ESP-NOW](https://randomnerdtutorials.com/esp-now-esp8266-nodemcu-arduino-ide/), and [MQTT](https://randomnerdtutorials.com/what-is-mqtt-and-how-it-works/).
2. The architecture requires [Soft Access Point](https://github.com/rsiyanwal/ESP8266-as-SoftAP) and [MAC address](https://github.com/rsiyanwal/NodeMCU-MAC-Address) of the devices that are using ESP-NOW protocol. We used ESP8266 as the device for creating that network. 
3. Using the [simulation](https://github.com/rsiyanwal/iFogSim-Simulations-for-Fog-Based-Surviliance-Architecture), you can identify the most suitable devices for your architecture based on your specific requirements such as latency, energy consumption, and cost.

### Modules

![Module-Mapping-3](https://user-images.githubusercontent.com/11557572/236669425-7506a355-7a7f-48b2-bb17-483b0a258401.png)</br>
_(Module Mapping; [Rahul Siyanwal](https://github.com/rsiyanwal/))_

| Number | Module | Short Description | 
| ------------- | ------ | ----------------- | 
| I | [Motion-Capture](https://github.com/rsiyanwal/Handling-Motion-Sensor-With-ESPNOW) | Capturing a movement (MSD) | 
| II | [MSD-ESP-Sender](https://github.com/rsiyanwal/Handling-Motion-Sensor-With-ESPNOW) | Sending the MSD via ESP-NOW | 
| III | [MSD-ESPNOW-MQTT-Forwarder](https://github.com/rsiyanwal/ESPNOW-and-MQTT) | Forwarding MSD to a device for processing via MQTT | 
| IV | [Servo-Image-Module](https://github.com/rsiyanwal/MQTT-Servo-Camera) | Adjusting the angle of servo motor in the direction where MSD is detected | |
| V | [Picture-Capture](https://github.com/rsiyanwal/MQTT-Servo-Camera) | Clicking an image in the direction of MSD | |
| VI | Image-Processing | Preprocessing the Image / Run your own model |
| VII | [Image-Producer](https://github.com/rsiyanwal/Apache-Kafka-Transfer-Images) | Producing the Image via Kafka | |
| VIII | [Image-Broker](https://www.conduktor.io/kafka/starting-kafka/) | Kafka Broker | |
| IX | [Image-Consumer](https://github.com/rsiyanwal/Apache-Kafka-Transfer-Images) | Consuming the Image via End-User | |

The architecture consists of several modules: Motion-Capture, MSD-ESP-Sender, MSD-ESPNOW-MQTT-Forwarder, Servo-Image-Module, Picture-Capture, Image-Processing, Image-Producer, Image-Broker, and Image-Consumer. The Motion-Capture module uses PIR sensors to detect motion and the MSD-ESP-Sender module sends Motion Sensor Data (MSD) to another NodeMCU connected to APU via ESP-NOW. To forward the MSD packets to the microprocessor, which does not support ESP-NOW, the MSD-ESPNOW-MQTT-Forwarder module uses the MQTT protocol. Once the Servo-Image-Module rotates the camera toward the MSU that sent the MSD, the Picture-Capture module captures the image. After storing and processing the image, the Image-Producer module sends it to the broker using Apache Kafka. The Image-Broker module handles the broker, and the Image-Consumer module receives the image on the subscribed topic on the consumer device.
