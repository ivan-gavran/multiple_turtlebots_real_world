# Launching two turtlebots under namespaces with navigation stack [solved]
This repository contains the launch files to launch a (real-world) turtlebot under a namespace. (Which is a key step towards launching multiple turtlebots all sharing a single master. This part would also be added.) 
It is similar in spirit to [this repository](https://github.com/gergia/multiple_turtlebots_stage_amcl), where the same was done for the simulation in Stage simulator. 

As a side note, running multiple turtlebots under the same master can (according to experiences of others) result in the performance issues. (The alternative solution would be that each TurtleBot runs its own master and that certain topics are shared using [multimaster_fkie](http://wiki.ros.org/multimaster_fkie) or something similar. (In this solution too it is good, though not necessary, to have robots under namespaces).

Many thanks for the help in setting this up and debugging to amiller27 and baeckermeister.
