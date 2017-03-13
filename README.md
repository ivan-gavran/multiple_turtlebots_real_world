# Launching two turtlebots under namespaces with navigation stack [solved]
This repository contains the launch files to launch a (real-world) turtlebot under a namespace. (Which is a key step towards launching multiple turtlebots all sharing a single master. This part would also be added.) 
It is similar in spirit to [this repository](https://github.com/gergia/multiple_turtlebots_stage_amcl), where the same was done for the simulation in Stage simulator. 

As a side note, running multiple turtlebots under the same master can (according to experiences of others) result in the performance issues. (The alternative solution would be that each TurtleBot runs its own master and that certain topics are shared using [multimaster_fkie](http://wiki.ros.org/multimaster_fkie) or something similar. (In this solution too it is good, though not necessary, to have robots under namespaces).

Many thanks for the help in setting this up and debugging to amiller27 and baeckermeister.

-----

<br /><br /><br /><br />

This is the part describing typical problems I was facing before the solution was found (old README file, while this was still a work in progress):<br/>
The goal of this repository is to create a launch file for two turtlebots under namespaces with navigation stack. The similar attempt for stage simulator ended successfully in [this repository](https://github.com/gergia/multiple_turtlebots_stage_amcl).
In this attempt I failed to do it myself, and hope that we can together accomplish it and have it as a reference for future, as it seems to be a question that bothers many. Therefore, build upon! (of course, if you have a ready solution, just let us know, link it, add it or whatever you find suitable).<br/> Also, add to this README file your conclusions.

## First step
First and crucial step is to launch a single robot under namespace (once that is done, the rest should be pretty easy).

## Current state

**EDIT**:
as baeckermeister commented in the Issues section, he found the solution to the problem. I was not able to integrate it with this code (I failed few times and later I neglected it). Another integration attempt - this time to the end :) - is happening right now...

 Currently, the attempt to launch a single robot under namespace with amcl failed. The tf tree looks like [this](https://dl.dropboxusercontent.com/u/11955498/framesTurtlebotUnderNamespace.pdf). The link between */map* and *robot\_0/odom* is missing. Amcl should be publishing this connection.<br/><br/>
The messages from console are following:<br/>

*  */robot\_0/amcl: No laser scan received (and thus no pose updates have been published) for 1462444802.174762 seconds.  Verify that data is being published on the /robot\_0/scan topic.*  : checked, data is being published at /robot\_0/scan <br/>

*   */robot\_0/amcl: MessageFilter [target=robot\_0/odom ]: Dropped 100.00% of messages so far. Please turn the [ros.amcl.message\_notifier] rosconsole logger to DEBUG for more information.* : **This might be a key message**. If I set the logger level to debbug, I see something like  *Added message in frame /camera\_depth\_frame at time 1462446392.094, count now 100*.<br/> I guess the trouble is that it is using frame id /camer_depth_frame (the absolute one) instead of one relative to the namespace (_robot\_0 in this case_). I don't know how to fix it. I tried with using *openni2\_tf\_prefix.launch*, but doesn't help. <br/>
* _ /robot\_0/move\_base\_node: Timed out waiting for transform from robot\_0/base\_link to map to become available before running costmap, tf error: . canTransform returned after 0.101826 timeout was 0.1._ : I guess this one is just a consequence of previous ones.


