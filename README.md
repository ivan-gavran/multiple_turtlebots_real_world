# Running multiple robots in stage simulator with navigation stack
## Starting with two robots 
To start with two robots call `roslaunch multiple_robots_in_stage robots_in_stage.launch`. This will set two
robots in the map.
To give them a goal you can call `rostopic pub /robot_1/move_base_simple/goal geometry_msgs/PoseStamped '{header: {stamp: now, frame_id: "/map"}, pose: {position: {x: 2.0, y: -10, z: 0.0}, orientation: {w: 1.0}}}'` 
