替换系统内部的jdk
----------------------------
* 替换系统内部的jdk
环境：vagrant (Linux version 2.6.32-38-server (buildd@allspice) (gcc version 4.4.3 (Ubuntu 4.4.3-4ubuntu5) ) #85-Ubuntu SMP Wed Jan 25 14:12:17 UTC 2012)
系统自带的版本：java && javac 1.6.0_35

操刀:
* 找到/etc/profile
* 使用sudo vim /etc/profile
若文件里面没有设置JAVA_HOME CLASSPATH,并且JAVA_HOME里面的bin路径信息没有在PATH里面设置，
只要是以上几种情况，就需要设置了
 JAVA_HOME=/home/vagrant/jdk1.8
 PATH=$JAVA_HOME/bin:$PATH
 CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
 export PATH=$PATH:~/.composer/vendor/bin
 export JAVA_HOME
 export PATH
 export CLASSPATH
