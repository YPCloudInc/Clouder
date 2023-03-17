# fBuilder 使用者指南
網址 - [RUN](https://run.ypcloud.com) -> 登入 -> 選擇 "fBuilder" 然後點擊 "go" 以開始

Flow Builder (fBuilder) 是由 YPCloud 開發的低代碼編程環境，參考了 IBM 的 Node-RED

當您啟動一個流程時，消息將沿著節點鏈傳遞，直到達到終點，前一個節點的輸出將成為下一個節點的輸入。

---

## 簡介

- [使用者介面](#使用者介面)

- [基本節點](#基本節點)

- [QRun](#QRun)

- [流程導入與導出](#流程導入與導出)

### FlowBot 指南 (範例)

- [雙時鐘](https://github.com/YPCloudInc/Clouder/blob/main/md/twin.md)

- [聊天機器人](https://github.com/YPCloudInc/Clouder/blob/main/md/chatbot.md)

- [表單機器人](https://github.com/YPCloudInc/Clouder/blob/main/md/form.md)

### [範例](https://github.com/motebus/ultrabook/blob/main/Ultranet%20Apps/fBuilder/Sample%20Flows/Readme.md)

---

# 使用者介面

[<img src="https://i.imgur.com/V8hyXg5.png" width=1200 height=600>](https://run.ypcloud.com)

---

## 左欄 - 節點列表

  * 您將無法從調色板安裝節點，如果您對嘗試節點列表之外的節點感興趣，可以探索 [Node-RED](https://nodered.org/)。

---

## 中間 - 工作區

流程標籤 - [<img src="https://i.imgur.com/iOCKLDh.png" width=800 height=30>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/QSdg0nI.png" width=30 height=30>](https://run.ypcloud.com) - 新增標籤

[<img src="https://i.imgur.com/xXm16T3.png" width=30 height=30>](https://run.ypcloud.com) - 標籤列表

---

## 右上角 [<img src="https://i.imgur.com/KCUock7.png" width=150 height=30>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/SbNMST5.png" width=120 height=30>](https://run.ypcloud.com) - 點擊部署以在編輯後**保存**您的流程

登出 - [<img src="https://i.imgur.com/LVwWqqI.png" width=30 height=30>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/w56SCE1.png" width=30 height=30>](https://run.ypcloud.com) - 列表
> [<img src="https://i.imgur.com/Ovl4J96.png" width=200 height=600>](https://run.ypcloud.com)

---

## 右欄 - 流程管理窗口 [<img src="https://i.imgur.com/xEKRbxs.png" width=200 height=30>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/yf4T3Be.png" width=30 height=30>](https://run.ypcloud.com) - 資訊：包括"啟用/禁用流程"
> [<img src="https://i.imgur.com/UHPdPPh.png" width=230 height=250>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/BZNT7Ak.png" width=30 height=30>](https://run.ypcloud.com) - 幫助

> 範例：
> [<img src="https://i.imgur.com/s82Kq0t.png" width=200 height=600>](https://run.ypcloud.com) 
[<img src="https://i.imgur.com/ICqFXMv.png" width=200 height=600>](https://run.ypcloud.com) 
[<img src="https://i.imgur.com/uk6Nhu8.png" width=200 height=600>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/hxlCBls.png" width=30 height=30>](https://run.ypcloud.com) - 調試
> 範例：
> [<img src="https://i.imgur.com/u7tT20h.png" width=500 height=150>](https://run.ypcloud.com)

- 函數節點內容

msg.payload=
{
"content": "Hello World~",
}
return msg;


[<img src="https://i.imgur.com/uJXy3dz.png" width=30 height=30>](https://run.ypcloud.com) - 配置
> [<img src="https://i.imgur.com/EU3SoQz.png" width=200 height=300>](https://run.ypcloud.com)

[<img src="https://i.imgur.com/KB6AFa4.png" width=30 height=30>](https://run.ypcloud.com) - 整體
> [<img src="https://i.imgur.com/MoOSTGu.png" width=200 height=200>](https://run.ypcloud.com)

---

# 基本節點

## 提示

1. 雙擊每個節點以編輯內容，在完成時按每個節點的 [<img src="https://i.imgur.com/a1M9i9h.png" width=60 height=25>](https://run.ypcloud.com)

2. 您可以使用 "ctrl+c" 和 "ctrl+v" 來複製/粘貼節點

3. 您可以用滑鼠框選多個節點以移動或複製/粘貼

4. 在調試/離開頁面之前，點擊 [<img src="https://i.imgur.com/SbNMST5.png" width=100 height=25>](https://run.ypcloud.com)，否則您所做的更改將不會被保存，部署後按鈕變為藍色

5. 範例 - [<img src="https://i.imgur.com/7KWSIGM.png" width=110 height=45>](https://run.ypcloud.com) 
  - 如果出現 "紅色三角形"，則節點內容為空或json代碼中存在錯誤 
  - 如果出現 "藍色圓點"，則節點尚未"部署"，請點擊 [<img src="https://i.imgur.com/SbNMST5.png" width=100 height=25>](https://run.ypcloud.com)

---

## 節點表格

* [inject](#inject) [<img src="https://i.imgur.com/CLSpzfz.png" width=110 height=30>](https://run.ypcloud.com)

* [set](#set) [<img src="https://i.imgur.com/mrUJBKE.png" width=110 height=30>](https://run.ypcloud.com)

* [payload](#payload) [<img src="https://i.imgur.com/XlbGGpk.png" width=110 height=30>](https://run.ypcloud.com)

* [function](#function) [<img src="https://i.imgur.com/QX7O8PO.png" width=110 height=30>](https://run.ypcloud.com)

* [send](#send) [<img src="https://i.imgur.com/LQ1jsMD.png" width=110 height=30>](https://run.ypcloud.com)

* [call](#call) [<img src="https://i.imgur.com/cF7R86U.png" width=110 height=30>](https://run.ypcloud.com)

* [switch](#switch) [<img src="https://i.imgur.com/UuE2qCf.png" width=110 height=30>](https://run.ypcloud.com)

* [debug](#debug) [<img src="https://i.imgur.com/zdAEqm1.png" width=110 height=30>](https://run.ypcloud.com)

* [comment](#comment) [<img src="https://i.imgur.com/URNpYxU.png" width=110 height=30>](https://run.ypcloud.com)

* [on/ret event](#1) [<img src="https://i.imgur.com/6mbbHyl.png" width=110 height=30>](https://run.ypcloud.com) & [<img src="https://i.imgur.com/HCFQkIE.png" width=110 height=30>](https://run.ypcloud.com)

---

### | inject [<img src="https://i.imgur.com/CLSpzfz.png" width=110 height=30>](https://run.ypcloud.com)
> [<img src="https://i.imgur.com/sWgEnlW.png" width=120 height=35>](https://run.ypcloud.com)

* 它也被稱為 "時間戳" 節點，因為它可以在特定時間觸發

* 通常是一條鏈的第一個節點

* 部署後點擊節點左側的藍色按鈕以觸發

* "在 0.1/自定義秒後注入一次" 的選框表示部署後將自動注入一次

* 重複可自定義時間以重複執行鏈

> [<img src="https://i.imgur.com/ppCarhZ.png" width=500 height=700>](https://run.ypcloud.com)

---

