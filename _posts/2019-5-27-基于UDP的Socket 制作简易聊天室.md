---
layout:     post
title:      基于UDP的Socket 制作简易聊天室
subtitle:   基于UDP的Socket 制作简易聊天室
date:       2019-05-27
author:     BOBO
header-img: img/post-bg-debug.png
catalog: true
tags:
    - 网络
---

![在这里插入图片描述](https://camo.githubusercontent.com/a5bb934be70005792a0a5231ee84c18664565602/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303532373130343734323332372e706e67)
![在这里插入图片描述](68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303532373130343833333239312e706e673f782d6f73732d70726f636573733d696d6167652f77617465726d61726b2c747970655f5a6d46755a33706f5a57356e6147567064476b2c736861646f775f31302c746578745f6148523063484d364c7939696247396e4c6d4e7a5a473475626d56304c334678587a51784e5441774d6a49792c73697a655f31362c636f6c6f725f4646464646462c745f3730)
![在这里插入图片描述](https://camo.githubusercontent.com/1d7831fd5fed3584b401a91296b7264c758f5b08/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303532373130343735353135302e706e67)
![在这里插入图片描述](https://camo.githubusercontent.com/82f82cf3e827f2c60f511d3b3a7d55cd48e2a69a/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303139303532373130343830373338322e706e67)
```python
import socket
import time

def send_msg(udp_socket):
    '''
    发送数据
    '''
    msg = input('请输入要发送的数据:\n')
    dest_ip = input('请输入对方的ip地址:\n')
    dest_port = int(input('请输入对方端口号:\n'))
    udp_socket.sendto(msg.encode('utf-8'),(dest_ip,dest_port))



def resv_msg(udp_socket):
    '''
    接收数据
    '''
    # 接收的最大字节
    msg = udp_socket.recvfrom(1024)
    # 解码
    recv_ip = msg[1]
    recv_msg = msg[0].decode('utf-8')
    print('{}:{}'.format(recv_ip,recv_msg))





def main():
    '''
    创建UDP套接字
    '''
    udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
    '''
    绑定本地信息
    '''
    udp_socket.bind(('172.20.10.13',7890))
    while True:
        print('='*30)
        print('1:发送数据')
        print('2:接收数据')
        print('='*30)
        op_num = input('请输入要使用的功能')
        if op_num == '1':
            send_msg(udp_socket)
        elif op_num == '2':
            resv_msg(udp_socket)
        else:
            print('输入参数有误2秒退出')
            time.sleep(2)
            break

if __name__ == "__main__":
    main()     


```
