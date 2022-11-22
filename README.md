# certificate
数字证书深入理解及使用 </br>


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
