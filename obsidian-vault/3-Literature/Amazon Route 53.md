#aws #services 

一種 [[DNS]] Web服務
- 域名註冊：直接購買新域名，或移轉域名
- DNS服務：管理域名DNS路由，A紀錄、AAAA紀錄、CNAME紀錄
- 流量管理：提供多種模式
	- 加權路由
	- 基於延遲路由
	- 地理位置路由
	- 故障管理路由
- 健康檢查
- 服務集成

### 流程
1. Amazon Route 53 使用 DNS 解析來識別 domain相對應的IP 回傳給客戶。
2. 客戶透過 [[Amazon CloudFront]] 傳送到最近的節點
3. 再透過 Load Balancer 將封包傳送到 [[AWS EC2 |EC2]]

![[Pasted image 20240510015028.png]]