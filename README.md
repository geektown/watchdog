# watchdog
watch dog for RESTful api service use shell script.
this is inspired by https://github.com/kwhitefoot/watchdog. 

A simple bash script to keep a process running if it hangs or crashes.

The principle is simple: launch the process and then repeatedly check a api at intervals. If the api died then kill the process and relaunch it.

To use it just put the watchdog script in the path and execute it like this:

watchdog "command line to execute" "command line to shutdown the process" "a rest api" interval_of_seconds

where the command line can be anything but remember that ~ will not be expanded if you quote it and that you will probably need to quote it unless it is a bare command with no arguments. The same applies to the path to the activity file. The interval is in whole minutes.

For details please see the source.

# Simple usage
```shell
nohup ./watchdog "docker run -d --name app-alpine -p 80:80 d77dacb81895" "docker rm -f app-alpine" "http://localhost/" 30 > watchdog-app.log 2>&1 &
```
# Kill the watchdog
`pkill "app-alpine" ` or `kill -9 $(ps -ef | grep "nginx-alpine" | grep -v "grep" | awk '{print $2}') `

 
