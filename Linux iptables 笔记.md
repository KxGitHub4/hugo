### Linux iptables ufw 笔记
#### · iptables原理图解及表格
#### · UFW快速添加端口                                   
### Linux 中数据的流向Chain
[![图片来源](C:\Users\O\Desktop\PS\iptables chains.webp)](https://www.booleanworld.com/wp-content/webp-express/webp-images/doc-root/wp-content/uploads/2017/06/Untitled-Diagram.png.webp)


<h4>Table and Chain</h4>

|Table chain|INPUT|FORWARD|OUTPUT|PREROUTING|POSTROUTING|
|----|----|
|Filter|√|√|√|×|×|
|NAT|×|×|√|√|√|
|Managle|√|√|√|√|√|
|raw|×|×|√|√|×|
### 简单的NAT转换示例
```
iptables -t nat -A prerouting -p [tcp|udp] --dport [local port] -j dnat --to-destination [remote ip]
iptables -t nat -A postrouting -p [tcp|udp] -d [remote ip] -j snat --s-source [local ip]
```

<details>
<summary>UFW 快速添加端口</summary>
<code>
#!/bin/sh
UFW() { 
  for PORT in $PORTS
  do
     echo $PORT
  done
  for PORT in $PORTS
  do
     ufw allow $PORT
  done
}
PORTS=$@
UFW
</code>
</details>


>> 图片来源于 [](https://www.booleanworld.com/depth-guide-iptables-linux-firewall/)