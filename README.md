# Launching two turtlebots under namespaces with navigation stack 

The goal of this repository is to create a launch file for two turtlebots under namespaces with navigation stack. The similar attempt for stage simulator ended successfully in [this repository](https://github.com/gergia/multiple_turtlebots_stage_amcl).
In this attempt I failed to do it myself, and hope that we can together accomplish it and have it as a reference for future, as it seems to be a question that bothers many. Therefore, build upon! (of course, if you have a ready solution, just let us know, link it, add it or whatever you find suitable).<br/> Also, add to this README file your conclusions.

## First step
First and crucial step is to launch a single robot under namespace (once that is done, the rest should be pretty easy).

## Current state
 Currently, the attempt to launch a single robot under namespace with amcl failed. The tf tree looks like [this](https://dl.dropboxusercontent.com/u/11955498/framesTurtlebotUnderNamespace.pdf). The link between */map* and *robot\_0/odom* is missing. Amcl should be publishing this connection.<br/><br/>
The messages from console are following:<br/>

*  */robot\_0/amcl: No laser scan received (and thus no pose updates have been published) for 1462444802.174762 seconds.  Verify that data is being published on the /robot\_0/scan topic.*  : checked, data is being published at /robot\_0/scan <br/>

*   */robot\_0/amcl: MessageFilter [target=robot\_0/odom ]: Dropped 100.00% of messages so far. Please turn the [ros.amcl.message\_notifier] rosconsole logger to DEBUG for more information.* : **This might be a key message**. If I set the logger level to debbug, I see something like  *Added message in frame /camera\_depth\_frame at time 1462446392.094, count now 100*.<br/> I guess the trouble is that it is using frame id /camer_depth_frame (the absolute one) instead of one relative to the namespace (_robot\_0 in this case_). I don't know how to fix it. I tried with using *openni2\_tf\_prefix.launch*, but doesn't help. <br/>
* _ /robot\_0/move\_base\_node: Timed out waiting for transform from robot\_0/base\_link to map to become available before running costmap, tf error: . canTransform returned after 0.101826 timeout was 0.1._ : I guess this one is just a consequence of previous ones.


