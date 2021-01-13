# Distribute same job to different slaves

Use [Throttle concurrent builds plugin](https://wiki.jenkins-ci.org/display/JENKINS/Throttle+Concurrent+Builds+Plugin):

1. Install the plugin
2. Go to Job configuration
3. Enable "Execute concurrent builds if necessary"
4. Enable "Throttle Concurrent Builds"
5. Set "Maximum Total Concurrent Builds=4"
6. Set "Maximum Concurrent Builds Per Node=1"
7. Enable "Restrict where this project can be run" and in the Label Expression add your label for the 4 slaves
