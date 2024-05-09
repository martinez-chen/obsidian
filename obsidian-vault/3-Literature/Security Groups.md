## Security Groups 安全群組
負責管理[[Amazon VPC|VPC]]中的子網路存取權限


如同大樓管理員一樣，確認是否可以進入，但不會確認是否可以傳出，無狀態

每個[[AWS EC2 |EC2]]都有自己的安全群組


### 比較

| ACL              | Security Groups |
| ---------------- | --------------- |
| 有狀態           | 無狀態          |
| 保護Subnetwork  | 保護EC2      |
| 限制進出         | 限制進入        |
| 檢查封包、傳送者 | 控制流量類型    | 

^aclvssecurity