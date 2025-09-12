# Kill process MAC OS


For macOS El Capitan and newer (or if your netstat doesn't support -p), use lsof:

lsof -i tcp:3000


Alternatively, you can use netstat:

netstat -vanp tcp | grep 3000


Once you have the PID (Process ID) use:

kill -9 <PID>
