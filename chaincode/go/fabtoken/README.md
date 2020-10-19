# fabric-fabtoken
在联盟链上构建token
--tls true --cafile /etc/hyperledger/artifacts/crypto-config/ordererOrganizations/greaspace.com/orderers/orderer.greaspace.com/msp/tlscacerts/tlsca.greaspace.com-cert.pem

测试命令：

//CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=fabtoken:0 ./fabtoken

注册链码
//peer chaincode install -p github.com/hyperledger/fabric/singlepeer/chaincode/go/fabtoken/ -n fabtoken -v 0
	
实例化链码
//peer chaincode instantiate -n fabtoken -v 0 -c '{"Args":[]}' -C mychannel

// 注册管理员账户
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"initLedger","Args":[]}' --tls true --cafile /etc/hyperledger/artifacts/crypto-config/ordererOrganizations/greaspace.com/orderers/orderer.greaspace.com/msp/tlscacerts/tlsca.greaspace.com-cert.pem

//创建账户 参数 ： (1)账户名
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"createAccount","Args":["liyi"]}'

//创建代币 (1) 代币全称 (2) 代币简称 (3) 代币总量 (4) 代币生成以后持有人 (5) 是否锁仓
// peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"initCurrency","Args":["Netkiller Token","VKT","1000000.9999","greavankia","false"]}' --tls true --cafile /etc/hyperledger/artifacts/crypto-config/ordererOrganizations/greaspace.com/orderers/orderer.greaspace.com/msp/tlscacerts/tlsca.greaspace.com-cert.pem
		
//锁仓某个代币 (1) 代币简称 (2) 是否锁仓 (3) 操作人
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"setLock","Args":["VKT","true","greavankia"]}'

//转账 (1) 发送人(2) 接收人(3) 代币名(4)发送代币量(5)备注
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"transferToken","Args":["greavankia","liyi","VKT","12.584","memo"]}' --tls true --cafile /etc/hyperledger/artifacts/crypto-config/ordererOrganizations/greaspace.com/orderers/orderer.greaspace.com/msp/tlscacerts/tlsca.greaspace.com-cert.pem

//冻结账户 (1) 要冻结的账户 (2) 是否冻结 (3) 操作人
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"frozenAccount","Args":["netkiller","true","greavankia"]}'

//代币增发 (1)代币名称(2)增发数量(3)操作人，也是代币增发接收人
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"mintToken","Args":["VKT","5000","greavankia"]}'

//代币销毁 (1)代币名称(2)回收数量(3)回收的账户（回收谁的代币）(4)操作人
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"burnToken","Args":["VKT","5000","liyi","greavankia"]}'

//查询指定账户指定代币 (1)查询账户 （2） 代币名称
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"balance","Args":["greavankia","VKT"]}'

//查询某个用户所有资金 (1)账户名
//peer chaincode query -C mychannel -n fabtoken -c '{"function":"balanceAll","Args":["greavankia"]}' --tls true --cafile /etc/hyperledger/artifacts/crypto-config/ordererOrganizations/greaspace.com/orderers/orderer.greaspace.com/msp/tlscacerts/tlsca.greaspace.com-cert.pem

//查询指定代币交易记录 (1)代币名称
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"tokenHistory","Args":["VKT"]}'
//查询指定用户指定代币交易记录 (1)代币名称(2)用户名
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"userTokenHistory","Args":["VKT","greavankia"]}'
//查询某个key 历史交易 (1)代币名称
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"tokenHistory","Args":["VKT"]}'

//查看某个账户(1)账户名
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"showAccount","Args":["greavankia"]}'

//查看所有代币
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"showToken","Args":[]}'

//查看代币的所有持有用户
//peer chaincode invoke -C mychannel -n fabtoken -c '{"function":"showTokenUser","Args":["VKT"]}'

