*print kernel messages such as oom*
dmesg 
 
#attach to proces to get info about system calls - useful for a hung process
strace -p <pid>
 
#show memory consumption (physical and swap)
free 
 
#show disk space consumption
df -h 
 
#real time mem and cpu usage
#use shift+f, then select Mem or CPU and hit s for sorting, hit q to go to sorted list
top
 
#process list, with optional filtering
ps aux | grep <process name>
 
#get stack trace of mono process
kill -QUIT <pid> 
 
#display list of open files by PID
lsof
 
#check if the system is currently busy - load average in the last 1, 5, 15 mins
uptime
 
#show list of tcp connections
netstat -t
 
#exit code for last command
echo $?
