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

### | set [<img src="https://i.imgur.com/mrUJBKE.png" width=110 height=30>](https://run.ypcloud.com)
* 設置裝置名稱（例如您的容器），將“EiName”字段設置為您想要的名稱

* 然後將注入節點連接到設置節點，部署並單擊按鈕

* 裝置現在設置為該名稱

> [<img src="https://i.imgur.com/5N7rr5q.png" width=300 height=200>](https://run.ypcloud.com)

---

### | payload [<img src="https://i.imgur.com/XlbGGpk.png" width=110 height=30>](https://run.ypcloud.com)
* 配置其他 Motechat 裝置可以接收的有效載荷

* 它是 JSON 格式的

---

### | function [<img src="https://i.imgur.com/QX7O8PO.png" width=110 height=30>](https://run.ypcloud.com)
* 基本節點中最通用的節點之一

* 允許對傳遞的消息運行 JavaScript 代碼

* 默認情況下，消息作為名為 msg 的對象傳入，並且函數將使用 `return msg;` 行返回輸入

* 返回“null”結束流程

* 只要返回一個 msg 對象，就可以多種方式工作，返回其他任何內容都會導致錯誤。

---

### | send [<img src="https://i.imgur.com/LQ1jsMD.png" width=110 height=30>](https://run.ypcloud.com)
> [<img src="https://i.imgur.com/Y9R4kge.png" width=120 height=35>](https://run.ypcloud.com)

* 向其他設備或通道發送有效載荷。

* 發送節點有兩個輸出端口：頂部的用於成功發送，底部的用於錯誤

* 通過 >>xxx 發送 DDN 和主題由 xxx://xxx（例如：>>comm,tg://-12345678）

---

### | call [<img src="https://i.imgur.com/cF7R86U.png" width=110 height=30>](https://run.ypcloud.com)
* 可用於請求多個 Motechat 配置設備的服務

* 這將用於獲取存儲在 YPCloud 的 Object Store 中的信息

---

### | switch [<img src="https://i.imgur.com/UuE2qCf.png" width=110 height=30>](https://run.ypcloud.com)
* 根據條件將消息路由到不同的輸出端口

* 可以根據特定條件選擇不同的輸出路徑

---

### | debug [<img src="https://i.imgur.com/zdAEqm1.png" width=110 height=30>](https://run.ypcloud.com)
> [<img src="https://i.imgur.com/jJW9AuB.png" width=120 height=35>](https://run.ypcloud.com)

選項
> [<img src="https://i.imgur.com/AQMj9hI.png" width=400 height=300>](https://run.ypcloud.com) [<img src="https://i.imgur.com/hkZe0nE.png" width=400 height=300>](https://run.ypcloud.com)

---

### | comment [<img src="https://i.imgur.com/URNpYxU.png" width=110 height=30>](https://run.ypcloud.com)
* 用於為流程添加文本註釋

---

### <h3 id="1">| on/ret event</h3> [<img src="https://i.imgur.com/6mbbHyl.png" width=110 height=30>](https://run.ypcloud.com) & [<img src="https://i.imgur.com/HCFQkIE.png" width=110 height=30>](https://run.ypcloud.com)
它用於在容器上接收來自其他容器的 Motechat 消息

* 這些節點的連接方式如下

> [<img src="https://i.imgur.com/6JCxVpb.png" width=450 height=120>](https://run.ypcloud.com)

---

# QRun

完成流程後，點擊[<img src="https://i.imgur.com/ZUuFPvK.png" width=20 height=20>](https://run.ypcloud.com)（右上角），然後選擇 "QRun"

選擇以下一個進行部署
[<img src="https://i.imgur.com/5zRsBQ9.png">](https://run.ypcloud.com)

如果您的頁面上顯示 "Deploy success" 或 "Timeout" 消息，則您的 QRun 已成功

如果顯示其他內容，則您的 QRun 失敗
> (尋求幫助)[<img src="https://i.imgur.com/GV3RRGW.png">](https://run.ypcloud.com)

在登出 fBuilder / 關機後，檢查您的流程是否正常運行（通過 Telegram Group、ioc 等）
> 使用後請記得登出 fBuilder！

---

# 流程導入和導出

## 導入流程
導入 flow.json 或 xxx.flow

[<img src="https://i.imgur.com/U82C32z.png" width=790 height=437>](https://run.ypcloud.com)

粘貼您的流程或選擇流程文件

[<img src="https://i.imgur.com/ELGRqsg.png" width=790 height=437>](https://run.ypcloud.com)

---

## 導出流程
您可以導出特定節點或整個流程

您可以下載 json 文件或將 json 複製到剪貼板（& "ctrl + v" 直接粘貼到任何地方

[<img src="https://i.imgur.com/L8p0Qwt.png">](https://run.ypcloud.com)
