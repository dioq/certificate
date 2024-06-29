# 自签名C根证书

自签名证书,能模拟 CA 根证书

## 1、创建根证书私钥

openssl genrsa -aes256 -out ca.key 2048 </br>
input [ca passwords]  </br>

## 2、根据私钥生成证书申请文件csr

证数各参数含义如下: </br>
C-----国家（Country Name）  </br>
ST----省份（State or Province Name） </br>
L----城市（Locality Name）  </br>
O----公司（Organization Name） </br>
OU----部门（Organizational Unit Name） </br>
CN----产品名（Common Name） </br>
emailAddress----邮箱（Email Address）</br>
openssl req -new -sha256 -key ca.key -out ca.csr -subj "/C=CN/ST=SD/L=JN/O=QDZY/OU=Apple/CN=CA/emailAddress=example@gmail.com" </br>
input [ca passwords]  </br>

## 3、自签署证书(有效期10年)

openssl x509 -req -days 3650 -sha256 -extensions v3_ca -signkey ca.key -in ca.csr -out ca.cer </br>
input [ca passwords]  </br>
