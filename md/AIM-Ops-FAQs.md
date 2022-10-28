AIM Ops - FAQs
===

[TOC]

---

## aimops 頁面說明
- 偵測紀錄 (Scan) - 網頁檢查與模型檢查等各式掃描紀錄
- 值班報表 (Duty) - 掃描偵測與備份異常事件紀錄
- 每日報表 (Daily) - 每日掃描與備份總覽報告，包含成功/失敗筆數
- 系統備份 (Backup) - 每日系統資料備份紀錄
- 系統記錄 (Log) - 目前為預留空間
- 問題小幫手 (FAQs) - 維運操作常發生問題專區
- 使用者設定 (User) - https://aimops.nchc.org.tw 使用者權限管理

---

## 注意AIM VM扣錢 
- 請留意 "乒乓話網" (super@ypcloud.com) 帳號的錢包餘額, 並定期增加額度, 以供AIM服務VM運行費用扣款
- https://www.twcc.ai/
- https://iservice.nchc.org.tw/

##  VM Info
| 主機代號 |	用途	| VCS名稱	| url | 系統     | 	規格 |
| ---- | ---- | ---- | ---- | ---- | ---- | 
| aim |	ai-market 主機	| aimkt30  | https://ai-market.nchc.org.tw |	Ubuntu 20.04	| 32vCPU, 256G MEM, 10TB HDD |
|aim2nd |	aim 備援主機 |	aim2backup | https://aim.nchc.org.tw |	Ubuntu 20.04 |	32vCPU, 256G MEM, 10TB HDD |
| aimlab |	aim 開發主機 |	aimkt30lab | https://aimlab.nchc.org.tw |	Ubuntu 20.04 |	4vCPU, 32G MEM. 1TB HDD |
| aimops |	aim 維運主機 |	aimktops | https://aimops.nchc.org.tw |	Ubuntu 20.04	| 16vCPU, 128G MEM, 10TB HDD |
| aimknode (k11) |	aim 運算主機	| aimktknode | https://k11.ai-market.nchc.org.tw |	Ubuntu 20.04 | 32vCPU, 256G MEM, 5TB HDD |

### VM Backup
- twcc 映像檔 & 快照 不一樣 (兩個都需要備份)
- https://www.twcc.ai

> 服務列表(Services) > 虛擬運算(VCS) 
從列表中點選VM, 進入到詳細資訊頁面後點選"映像檔"進行備份


> 虛擬磁碟服務> 資料磁碟
從列表中點選資料磁碟, 進入到詳細資訊頁面後點選"快照"進行備份



---
## mk8s Ops - VM 注意事項
https://gitops.ypcloud.com/aimlab/aimlab-mk8s-sys

## Common mk8s Errors
https://gitops.ypcloud.com/aimkt/aimkt-20/aimkt/aimkt-doc/aimkt-ioc/-/blob/master/aimkt-3am.md


## mk8s Terminating Issues
https://gitops.ypcloud.com/aimlab/aimlab-mk8s-sys/-/blob/main/mk8s/terminating%20issue.md

## Backup and Restore DB 
https://gitops.ypcloud.com/aimops/ioc/rm

---
###### tags: `AIM`,`Ops`,`FAQ` 
---
> [YPCloud Inc.](https://www.ypcloud.com)
> [name=Shin]
> [time=2022-09-28]
