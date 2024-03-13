# HTTPS 通信过程

HTTPS数字证书得认证安全后才能使用

## SSL单向认证

服务器需要CA根证书、server证书、server私钥，客户端需要CA根证书      </br>

单向认证命令行:            </br>
服务器:                   </br>
openssl s_server -CAfile ca.cer -cert server.cer -key server.key -accept 22580          </br>
客户端:
openssl s_client -CAfile ca.cer -cert client.cer -key client.key -connect 127.0.0.1:22580       </br>

## 双向认证

服务器需要CA根证书、server证书、server私钥，客户端需要CA根证书，client证书、client私钥      </br>

双向认证命令行:         </br>
服务器:                 </br>
openssl s_server -CAfile ca.cer -cert server.cer -key server.key -accept 22580 -Verify 1        </br>
客户端:         </br>
openssl s_client -CAfile ca.cer -cert server.cer -key server.key -cert client.cer -key client.key -connect 127.0.0.1:22580          </br>
