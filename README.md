# certificate
数字证书产生的目的是为了做 RSA 加解密里的 public key 的安全分发.        </br>
数字证书组成部分: 公钥, 公钥描述信息, 签名信息         </br>
       签名信息: 消息摘要 被CA机构的私钥加密后的二进制数据              </br>
       消息摘要: 公钥和公钥描述信息 进行hash散列(如sha256)得到的二进制数据        </br>

工作原理: 终端设备(如:浏览器(Chrome,Edge),操作系统(Android, iOS,Mac OS, Windows)) 等都会内置 CA机构的公钥, 在进行RSA 公钥分发时 把对应的数字证书分发出去, 终端接收到数字证书后用 CA公钥解密签名信息得到消息摘要, 然后再将数字证书里的 公钥和公钥描述信息进行 hash 运算得到消息摘要, 将消息摘要和 CA公钥解密出的消息摘要 进行对比,如果一致说明证书未被篡改过、可以放心使用数字证书里包含的公钥。    </br>
安全原理: CA 私钥加密的内容只能由 CA 公钥解密, 如果CA私钥是安全的则由CA私钥加密的数字证书便是安全的.     </br>

## 证书及格式介绍
PKCS 全称是 Public-Key Cryptography Standards ,是由 RSA 实验室与其它安全系统开发商为促进公钥密码的发展而制订的一系列标准,PKCS 目前共发布过 15 个标准。  </br>
常用的有: </br>
PKCS#7  Cryptographic Message Syntax Standard             	常用的后缀是: .P7B .P7C .SPC  </br>
PKCS#10 Certification Request Standard  </br>
PKCS#12 Personal Information Exchange Syntax Standard       常用的后缀有: .P12 .PFX   </br>

X.509是常见通用的证书格式。所有的证书都符合为Public Key Infrastructure (PKI) 制定的 ITU-T X509 国际标准。 </br>
X.509 DER 编码(ASCII)的后缀是:  .DER .CER .CRT    </br>
X.509 PAM 编码(Base64)的后缀是: .PEM .CER .CRT    </br>

注释:   </br>
.der .cer 文件一般是二进制格式的,只放证书,不含私钥   </br>
.crt 文件可能是二进制的,也可能是文本格式的,应该以文本格式居多,功能同 der和cer    </br>
.pem 文件一般是文本格式的,可以放证书或者私钥,或者两者都有,如果只含私钥的话,一般用.key扩展名,而且可以有密码保护    </br>
.pfx .p12 文件是二进制格式,同时含私钥和证书,通常有保护密码   </br>

## 证书格式转换
### X.509 到 PKCS#12
openssl pkcs12 -export -inkey private.key -in cert.cer -out cert.p12    </br>
### PKCS#12 到 X.509
openssl pkcs12 -nocerts -nodes 	-in cert.p12 -out private.key 			    # 导出私钥      </br>
openssl pkcs12 -clcerts -nokeys -in cert.p12 -out cert.pem           	  # 导出数字证书   </br>
### X.509 内部格式间转换
openssl rsa -in temp.key -out temp.pem                                  # key 转 pem   </br>
openssl x509 -in tmp.crt -out tmp.pem                                   # crt 转 pem   </br>
openssl x509 -outform der -in cert.pem -out cert.cer                    # pem 转 cer   </br>
#### java(包括Android)使用 jks 格式,用keytool将 cer 转成 jks
keytool -import -alias mycert1 -file server.cer  -keystore server.jks
