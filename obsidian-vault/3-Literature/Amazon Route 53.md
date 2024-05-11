#aws #services 

一種 [[DNS]] Web服務，具備管理網域名稱的 DNS 紀錄，也可以直接在 Route 53 註冊新的網域名稱。


1. Amazon Route 53 使用 DNS 解析來識別 domain相對應的IP 回傳給客戶。
2. 客戶透過 [[Amazon CloudFront]] 傳送到最近的節點
3. 再透過 Load Balancer 將封包傳送到 [[AWS EC2 |EC2]]

![[Pasted image 20240510015028.png]]