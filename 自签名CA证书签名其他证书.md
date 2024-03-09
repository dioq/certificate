# 模拟生CA证书
https证书厂商一般都会有一个根证书，这里模拟生成了https厂商根证书

## 一、生成CA证书
### 1、创建CA证书私钥 </br>
openssl genrsa -aes256 -out ca.key 2048 </br>
input [ca passwords]  </br>
### 2、根据私钥生成证书申请文件csr
证数各参数含义如下: </br>
C-----国家（Country Name）  </br>
ST----省份（State or Province Name） </br>
L----城市（Locality Name）  </br>
O----公司（Organization Name） </br>
OU----部门（Organizational Unit Name） </br>
CN----产品名（Common Name） </br>
emailAddress----邮箱（Email Address）</br>
openssl req -new -sha256 -key ca.key -out ca.csr -subj "/C=CN/ST=SD/L=JN/O=QDZY/OU=Apple/CN=CA/emailAddress=zhendong2011@live.cn" </br>
input [ca passwords]  </br>
### 3、自签署证书(有效期10年)
openssl x509 -req -days 3650 -sha256 -extensions v3_ca -signkey ca.key -in ca.csr -out ca.cer </br>
input [ca passwords]  </br>

## 二、 生成服务器证书
### 1、创建服务器私钥 
openssl genrsa -aes256 -out server.key 2048  </br>
input [server passwords]  </br>
### 2、根据私钥生成证书申请文件csr
openssl req -new -sha256 -key server.key -out server.csr -subj "/C=CN/ST=SD/L=JN/O=QDZY/OU=Apple/CN=SERVER/emailAddress=zhendong2011@live.cn"    </br>
input [server passwords]  </br>
### 3、使用CA证书签署服务器证书申请文件csr
openssl x509 -req -days 3650 -sha256 -extensions v3_req  -CA  ca.cer -CAkey ca.key  -CAserial ca.srl  -CAcreateserial -in server.csr -out server.cer </br>
input [ca passwords]  </br>


## 三、生成客户端证书
### 1、生成客户端私钥
openssl genrsa -aes256 -out client.key 2048    </br>
input [client passwords]  </br>
### 2、根据私钥生成证书申请文件csr
openssl req -new -sha256 -key client.key  -out client.csr -subj "/C=CN/ST=SD/L=JN/O=QDZY/OU=Apple/CN=CLIENT/emailAddress=zhendong2011@live.cn"    </br>
input [client passwords]  </br>
### 3、使用CA证书签署客户端证书申请文件csr
openssl x509 -req -days 3650 -sha256 -extensions v3_req  -CA  ca.cer -CAkey ca.key  -CAserial ca.srl  -CAcreateserial -in client.csr -out client.cer   </br>
input [ca passwords]  </br>
