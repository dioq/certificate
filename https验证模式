# HTTPS 通信过程 数字证书 得认证安全后才能使用,有多种认证方式

## 对于SSL单向认证：
服务器需要CA证书、server证书、server私钥，客户端需要CA证。
## 对于SSL双向认证：
服务器需要CA证书、server证书、server私钥，客户端需要CA证书，client证书、client私钥。

## 生成数字证书后可进行测试
### 单向认证命令行：
#### 服务器：
openssl s_server -CAfile ca.cer -cert server.cer -key server.key -accept 22580
#### 客户端：
openssl s_client -CAfile ca.cer -cert client.cer -key client.key -connect 127.0.0.1:22580

### 双向认证：
#### 服务器：
openssl s_server -CAfile ca.cer -cert server.cer -key server.key -accept 22580 -Verify 1
#### 客户端：
openssl s_client -CAfile ca.cer -cert server.cer -key server.key -cert client.cer -key client.key -connect 127.0.0.1:22580
