### 2017 NASA Swarmathon Competition Rules

The goal of the 2017 NASA Swarmathon competition is to program a swarm of robots to search a square arena to find and collect as many resources as possible in a fixed period of time. The competition rules are described below. Note that the number of robots, the dimensions of the arena, and the length of time of each round are best estimates at this time, but may change before the final competition due to logistical considerations at NASA Kennedy Space Center. The Physical and Virtual competition rules are identical.

- Tournament structure

    - There will be three competition rounds: preliminary, semi-final, and final:

        - The preliminary rounds will require 3 robots to search an approximate 15 x 15 meter walled arena for a maximum of 256 resources over two periods of 30 minutes each. The top eight teams whose robots find and collect the most resources during the two preliminary rounds will move on to the semi-final round.
    
        - The semi-final round will require 6 robots to search an approximate 22 x 22 meter walled arena for a maximum of 256 resources over a period of 30 minutes. The top four teams whose robots find and collect the most resources during the semi-final round will move on to the final round.

        - The final rounds will require 6 robots to search an approximate 22 x 22 meter walled arena for a maximum of 256 resources over a period of 1 hour.
        
        Refer to the "Breaking a tie" subsection near the bottom of this document for rules in the case of a tie score during a given round. Note that the exact number and spatial distribution of resources in each round will not be revealed in advance of the competition.

- Resources

    - Resources are represented by AprilCubes, foam cubes with [AprilTag](https://april.eecs.umich.edu/wiki/index.php/AprilTags) fiducial markers on all six sides. Note that all AprilTags on all sides are identical: every side is adhered with the [AprilTag from the 36h11 family with id=0](https://github.com/BCLab-UNM/Swarmathon-ROS/blob/master/simulation/models/at0/materials/textures/atag-0.png).

    - Resources will be randomly placed around the arena. Resources may be placed in a uniform distribution, such that the probability of encountering each resource is equal, or in a non-uniform distribution, in which some resources will be grouped together. The resource distribution will be selected at random before each round, meaning that neither the exact locations of resources, nor the number of clusters of resources, will not be disclosed to teams in advance of the competition.

    - "Collecting a resource" is defined as delivering an AprilCube to the [collection zone](https://github.com/BCLab-UNM/Swarmathon-ROS/blob/master/simulation/models/collection_disk/materials/textures/collection_disk.pdf) at the center of the arena. In order to receive credit for the collection at the end of the round, the AprilCube must be either inside of the 1 x 1 meter square collection zone, or touching the thick black line that designates the edge of the 1 x 1 meter square collection zone. If resources that were previously delivered are accidentally pushed out of the collection zone by other robots during the round, those resources will no longer count toward the total resources collected by a team during a given round. Scoring for each round will only occur at the end of the round, after all robot motion has been stopped.
    
    - Scoring decisions of official competition judges are final.

    - Resources will not be placed inside the collection zone, nor will they be placed within 50 cm of the arena wall.

- During the competition

    - Teams may not communicate with their robots in any way during the competition. All robot actions must be autonomous, and starting and stopping of autonomous motion must only be initiated by the official competition staff.

    - The robots used for the competition will be physically identical to the 3 robots provided to each team.
    
    - If robot-robot communication is required, all communication must be done via ROS topics and the ROS master. Robots will not be aware of each other's hostnames or IP addresses, but rather only the hostname and IP of the ROS master.

- During each round

    - Each team’s code will be uploaded to the robots before each round.

    - At the beginning of each round, each team’s robots will be placed **roughly** 50 cm from the edge of the collection zone and **roughly** equidistant from one another, with each robot facing in toward the center of the collection zone, then the robots will be turned on. Teams should **not** expect any robot to be placed in any specific position, nor should they expect the arena itself to be oriented in any specific direction.
    
    - Each robot should be prepared to receive and react to a start signal in the form of the published value ```2``` on the ```/robotName/mode``` topic, as well as a stop signal in the form of the published value ```1``` on the same topic (identical to the autonomous/manual radio button functionality in the GUI).
    
    - Each robot must publish a string on the `/robotName/status` topic. This string (set to `online` by default in the Swarmathon-ROS code base) should uniquely identify each team so that competition staff can ensure that the correct code is being run. For example, if a UNM team were to compete in the competition, they might publish the string `UNM: Go Lobos!` on the `/robotName/status` topic in order to uniquely identify their code.

    - In the Physical Competition, robots that become stuck due to any fault of the arena, or robots that collide with one another and become stuck, will be separated and placed nearby their original locations by line judges. The line judge will decide whether the arena is at fault. No intervention will occur in the Virtual competition.

    - Each robot must operate at a safe speed in order to avoid damage from collisions with the walls and with other robots. The maximum allowable velocity for the physical robots is 1.0 m/s linear and 1.0 m/s angular; the maximum velocity for the simulated robots is 1.5 m/s linear and 8.0 cm/s angular (this cap includes the simulated scaling factor). At the discretion of Physical Competition judges, robots that repeatedly crash into walls or each other at high speeds will be removed from the arena for the remainder of the period.
    
- Breaking a tie

    - In the event of a tie for 8th place at the end of the preliminary round, for 4th place at the end of the semi-final round, or for the winner at the end of any of the final rounds, the tied teams will compete head-to-head during a special tie breaker match. For this match, each team's robots and resources will be reset within their respective arenas. The team whose robots find and collect the most resources in 10 minutes will move on to the next round. If teams are still tied at the conclusion of the overtime match, the match will continue in a "sudden death" form, where the first team to score wins.

- Modifying the Swarmathon-ROS code base

    - Teams participating in the Physical competition are encouraged to modify any parts of the Swarmathon-ROS code base, including adding or deleting ROS packages and adjusting the Gazebo model files to better replicate the capabilities of their physical robots, **with the exception** of `/src/rqt_rover_gui`, which should **not** be modified. You may modify the `/misc/rover_onboard_node_launch.sh` startup script, but **do not** change the name of the script itself. All committed code that is pushed to a team's GitHub repository by the cutoff date will be pulled and run onboard robots during the Physical competition.
    
    - Teams participating in the Virtual competition are also allowed to modify any parts of the code base, including adding or deleting ROS packages, **with the exception** of `/simulation`, `/src/rqt_rover_gui`, and `/src/gazebo_plugins`, which **may not** be modified.
