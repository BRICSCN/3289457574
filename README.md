
<!-- markdownlint-disable -->




## Table of contents[![](https://raw.githubusercontent.com/aregtech/areg-sdk/master/docs/img/pin.svg)](#table-of-contents)
- [Team members](#Team-members)
- [Problems to solve](#Problems-to-solve)
- [Project solution](#Project-solution)
- [Advantage and innovation](#Advantage-and-innovation)
---
## Team members[![](https://raw.githubusercontent.com/aregtech/areg-sdk/master/docs/img/pin.svg)](#Usage-modes)



Name: Li Xiang
Role：Software engineer & Pilot
Responsibilities：Write code for autonomous fligt、multi-objects recognition system、autonomous tracking system and obstacle avoidance system，UAV flight & maintenance。

<p align="center">
    <img width="600" src="https://github.com/BRICSCN/3289457574/blob/main/12/xinjian/%E5%A4%B1%E7%81%AB.gif" />
</p>

### Swarm in Blocks 2024



Swarm in Blocks is 

<p align="center">
    <img width="500" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/intro/blocksIDE.gif" />
</p>

<p align="center">
    <img width="500" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/intro/ring.gif" />
</p>


For more information on our project from last year, see our final article in [Swarm in Blocks 2022](https://clover.coex.tech/en/swarm_in_blocks.html). In addition, we also recommend watching our final video from last year, [Swarm in Blocks 2022 - Final Video](https://www.youtube.com/watch?v=5C-1rRnyiE8).



### What's new




| Problem | Our Solution |
| -------- | -------- |




> 📖 **Acess our [Gitbook](https://app.gitbook.com/s/C9O11TiXK1JPnlrpilLg/background-theory/system)!**

<div align="right">[ <a href="#table-of-contents">↑ to top ↑</a> ]</div>

---

## Problems to solve[![](https://raw.githubusercontent.com/aregtech/areg-sdk/master/docs/img/pin.svg)](#Usage-modes)


- *Project background：*
Drones can be useful in areas like large supermarkets 、museums and unmanned monitoring of warehouses where there are several threats, including: things lost, fires predicted, and thieves who are difficult to capture.

<p align="center">
    <img width="600" src="https://github.com/BRICSCN/3289457574/blob/main/12/xinjian/%E5%81%B7%E7%9B%97.gif" />
</p>

<p align="center">
    <img width="600" src="https://github.com/BRICSCN/3289457574/blob/main/12/xinjian/%E5%A4%B1%E7%81%AB.gif" />
</p>

<p align="center">
    <img width="600" src="https://github.com/BRICSCN/3289457574/blob/main/12/xinjian/%E8%BF%BD%E8%B8%AA%E6%96%B0%E9%97%BB.gif" />
</p>

---

## Project solution[![](https://raw.githubusercontent.com/aregtech/areg-sdk/master/docs/img/pin.svg)](#Usage-modes)


The Swarm in Blocks can be programmed either with the blocks interface or directly in Python and we developed three main launch modes, each one focused on a different application of the project, they are:


- *Planning Mode:* Its main goal is to allow the user to check the drones' layout, save and load formations, before starting the simulator or using real clovers. In order to need less computational power and avoid possible errors during the simulation.


<div align="right">[ <a href="#table-of-contents">↑ to top ↑</a> ]</div>

---

## Advantage and innovation[![](https://raw.githubusercontent.com/aregtech/areg-sdk/master/docs/img/pin.svg)](#New-Swarm-Features)


With our vision of solving the problems that most plague the deployment of a real swarm, we have developed several features (and even integrated platforms), below we will list our main developments:

### Homepage

Like last year, we really wanted to make it easier for the user to go through our platform. That's why this year we decided to restructure our Homepage, gathering our main features and functionalities.

<p align="center">
    <img width="700" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/homepage/homepage.gif"/>
</p>

### Swarm Station


The main feature from our platform is the *Swarm Station*, which is a **3d Web Visualizer** that shows in real time all the necessary information regarding the drones state, such as real time positioning and visualization, which clover is connected, the topics available and a lot more. Also, you can define a safe area to ensure each drones safety, forcing them to land in case they cross the forbidden area. The front end runs completely on the web browser, saving processing and installation resources. It also comes with a web terminal, allowing the user to open several instances of a terminal emulation in just one click.

<p align="center">
    <img width="700" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/swarm_station/vid01.gif"/>
</p>

This package uses the ROS suite `rosbridge_server` to establish a communication between the ROS environment and the web server. 

To run it, we recommend using **Firefox** browser to assure stability. But feel free to test it on other navigators. 

If you launched our `simulation.launch` from the `swarm_in_blocks` package, then you just have to run

    roslaunch swarm_station swarm_station.launch

Otherwise, you have to make sure that the `rosbridge_websocket` is running on port `9090`:
    
    roslanch rosbridge_server rosbridge_websocket.launch port:=9090 
    
For more detailed instructions on how to use each single feature from the Swarm Station, check our [Gitbook page about the station](https://swarm-in-blocks.gitbook.io/swarm-in-blocks/). 


### Swarm Collision Avoidance


When many drones move close to each other, collisions are very likely to occur. To avoid this problem, an algorithm was developed to avoid collisions between drones. When analyzing a collision, 3 types of scenario are possible, the case where one clover is stationary and the other in motion, the case where both are in motion and with parallel trajectories, and finally the case where both are in motion and with non-parallel trajectory.

To turn on the collision avoidance, it is necessary to run:

    rosrun swarm_collision_avoidance swarm_collision_avoidance_node.py

<p align="center">
    <img width="600" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/collision.gif" />
</p>


### Rasp Package


The Raspberry package was developed to instantiate a node that will be responsible for collecting essential processing, memory and temperature information from the raspberry and send it to the Swarm Station. It's the package that should be put on the `catkin_ws/src/` directory of each Raspberry Pi, because it also contains the `realClover.launch` needed to launch the swarm on real life.

### Swarm FPV


This package is a reformulation of one of the CopterHack 2022 implementations, the **Swarm First Person Viewer**. This year, we decided to restart its structure, making it run also completely on the web to integrate with the Swarm Station. It also depends on the `rosbridge_websocket` running on the port `9090` (default).

<p align="center"> 
    <img width="600" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/fpv_2023.gif"/>
</p>

### Real Swarm

In order to fly a real swarm using clover, we decided to take an approach of putting every clover on the same ROS network / environment so that the master could talk to each one of them. 

We did this by separating each drone topics / nodes / services with namespaces. The goal is to achieve the same effect as the simulation that we've done in **CopterHACK 2022**, so each drone would have its own `/cloverID` namespace, and the ID is the identifier for each drone. 

In other wods, instead of just `simple_offboard` node for a single drone, we'd now have `/clover0/simple_offboard`, `/clover1/simple_offboard` and so on.

To launch it, you need to first stop clover's default daemon, and then connect all raspberrys to the same network. After that, you should connect all their `roscore` to the same IP address (the master's), and then launch the `realClover.launch` file passing the `ID` arguement as a parameter. Again, for more detailed information on how this works, please check out our [gitbook](https://swarm-in-blocks.gitbook.io/swarm-in-blocks/):

    sudo systemctl stop clover
    roslaunch rasp_pkg realClover.launch ID:=0
 

<p align="center">
    <img width="500" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/swarm_real/swarm.gif"/>
</p>

> **Note:** We are aware that in the video the calibration of the drone control is not ideal, however, the objective of this test was really to validate the operation of the swarm in a real environment (which was actually done).


<div align="right">[ <a href="#table-of-contents">↑ to top ↑</a> ]</div>

---

## 1234[![](https://raw.githubusercontent.com/aregtech/areg-sdk/master/docs/img/pin.svg)](#Conclusion)


Engineering and robotics challenges have always been the main driver of Team Athena, from which we seek to impact society through innovation. Last year, during CopterHack 2022, there was no lack of challenges of this type, and in them we grew and exceeded our limits, all to deliver the best possible project: **Swarm in Blocks**. All the motivation to facilitate a task as complex as the manipulation of swarms of drones, even through block programming, delighted us a lot and we hope that it delights all our users.

With that came the Swarm in Blocks 2.0, which brought with it innovations that optimized the clover's flight control and that could allow for greater emotions in the handling of the drone, in addition to focusing on greater flight safety.
The Swarm in Blocks 2.0 presents new features for this year, such as the Web terminal, First Person View (FPV), Collision Avoidance, Clover UI and Swarm Station.
However, the work will not stop there. Our goal is to further improve our system and next steps include validating Collision Avoidance outside the simulated world and performing performance tests with network communication solutions to optimize Real Swarm.

Finally, we thank the entire COEX team that made CopterHack 2023 possible and all the support given during the competition. We are Team Atena, creator of the Swarm in Blocks platform and we appreciate all your attention!

<div align="right">[ <a href="#table-of-contents">↑ to top ↑</a> ]</div>

---
## The Atena Team 

Atena Team 2023 (Swarm in Blocks 2.0):

- Agnes Bressan de Almeida : [Github](https://github.com/AgnesBressan), [LinkedIn](https://www.linkedin.com/in/agnes-bressan-148615262/)
- Felipe Tommaselli: [Github](https://github.com/Felipe-Tommaselli), [LinkedIn](https://www.linkedin.com/in/felipe-tommaselli-385a9b1a4/)
- Gabriel Ribeiro Rodrigues Dessotti : [Github](https://github.com/dessotti1), [LinkedIn](https://www.linkedin.com/in/gabriel-ribeiro-rodrigues-dessotti-8884a3216)
- José Carlos Andrade do Nascimento: [Github](https://github.com/joseCarlosAndrade), [LinkedIn](https://www.linkedin.com/in/jos%C3%A9-carlos-andrade-do-nascimento-71186421a)
- Lucas Sales Duarte : [Github](https://github.com/LucasDuarte026), [LinkedIn](https://www.linkedin.com/in/lucas-sales-duarte-a963071a1)
- Matheus Della Rocca Martins : [Github](https://github.com/MatheusDrm), [LinkedIn](https://www.linkedin.com/in/matheus-martins-9aba09212/)
- Nathan Fernandes Vilas Boas : [Github](https://github.com/uspnathan), [LinkedIn](https://www.linkedin.com/mwlite/in/nathan-fernandes-vilas-boas-047616262)

<p align="center">
    <img width="500" src="https://github.com/Grupo-SEMEAR-USP/swarm_in_blocks/blob/master/assets/atena_team.JPG"/>
</p>


In honor of Atena Team 2022:

- Guilherme Soares Silvestre : [Github](https://github.com/guisoares9), [LinkedIn](https://www.linkedin.com/in/guilherme-soares-silvestre-76570118b/)
- Eduardo Morelli Fares: [Github](https://github.com/faresedu), [LinkedIn](https://www.linkedin.com/in/eduardo-fares-a271561a0/)
- Felipe Tommaselli: [Github](https://github.com/Felipe-Tommaselli), [LinkedIn](https://www.linkedin.com/in/felipe-tommaselli-385a9b1a4/)
- João Aires C. F. Marsicano: [Github](https://github.com/Playergeek181), [LinkedIn](https://www.linkedin.com/in/joao-aires-correa-fernandes-marciano-53b426195/)
- José Carlos Andrade do Nascimento: [Github](https://github.com/joseCarlosAndrade), [LinkedIn](https://www.linkedin.com/in/jos%C3%A9-carlos-andrade-do-nascimento-71186421a)
- Rafael Saud C. Ferro: [Github](https://github.com/Rafael-Saud), [LinkedIn](https://www.linkedin.com/in/rafael-saud/)


<div align="right">[ <a href="#table-of-contents">↑ to top ↑</a> ]</div>
