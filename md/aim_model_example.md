# 模型訓練範例

1. 點擊模型管理頁面

![](https://i.imgur.com/27BbrWC.png)

2. 進入我的模型的訓練模型頁面, 建立一個**註冊模型**

例: Model name: MNIST手寫辨識

![](https://i.imgur.com/C5SsJMJ.png)

3. 點擊MLFLOW介面

![](https://i.imgur.com/ZPPR4po.png)

**mlflow和s3連結說明**

* 預設會開啟一個儲存貯體名稱(Bucket)

例: Artifact Location: s3://0ea2e731-2a38-46dd-a920-3c97de8c4b43/0

Artifact Location: s3://{儲存貯體名稱}/{資料夾}

![](https://i.imgur.com/g5OySHv.png)

* 點擊物件儲存管理

![](https://i.imgur.com/aOF3OA5.png)


* 查看相對應的儲存貯體名稱

![](https://i.imgur.com/tcvAyuJ.png)


* 建立一個新的儲存貯體(Bucket)

例: Bucket: mlflow-mnist-trained

![](https://i.imgur.com/NmszZ3m.png)

* 回到mlflow頁面, 建立新的實驗, 並且輸入新開的儲存貯體名稱(Bucket)

例:

Experiment Name: mnist

Artifact Location: s3://mlflow-mnist-trained

Artifact Location: s3://{儲存貯體名稱}

![](https://i.imgur.com/T6Ei4EY.png)

* 該實驗(mnist)的訓練結果都會將物件儲存在新的儲存貯體(mlflow-mnist-trained)

![](https://i.imgur.com/Xarlqpo.png)

4. 移動到mlflow頁面後, 點擊**Models**確認建立的**註冊模型**

![](https://i.imgur.com/bT4asDi.png)

5. 點擊**資料市集**

![](https://i.imgur.com/W83OuGJ.png)

6. 從資料市集訂閱相關資料集

例: MNIST

![](https://i.imgur.com/PXJeYeh.png)

7. 點擊**資料集管理**

![](https://i.imgur.com/cthfpud.png)

8. 點擊**預覽**訂閱的資料集

![](https://i.imgur.com/rn3NDrk.png)

9. 點擊**探索**後點擊**複製資料集**
例: mnist-in-csv.zip

![](https://i.imgur.com/S2K6uYB.png)

10. 選擇jupyter容器後點擊**複製**, 將資料複製到開發環境中

![](https://i.imgur.com/XY6EckK.png)

**建立jupyter環境說明**

* 若還沒有建立jupyter容器, 點擊前往jupyter

![](https://i.imgur.com/zSwQGAj.png)

* 建立jupyter容器

點擊+

![](https://i.imgur.com/1EQR4n1.png)

輸入名稱和描述, 選擇映像檔和規格, 下一步

![](https://i.imgur.com/7Nl7NUL.png)

點擊建立

![](https://i.imgur.com/nxTLZ1T.png)

點擊重新整理

![](https://i.imgur.com/GlGrEM8.png)

進度: Ready, 表示jupyter建立完成

![](https://i.imgur.com/EysyqGF.png)

點擊執行

![](https://i.imgur.com/W2TN0Ue.png)

開啟jupyter

![](https://i.imgur.com/MtqDYbE.png)

![](https://i.imgur.com/nOinkJ8.png)

11. 前往jupyter查看複製的資料

![](https://i.imgur.com/BcJY32D.png)

12. 開啟terminal

![](https://i.imgur.com/NPPH5W1.png)

13. 解壓縮資料
指令: unzip mnist-in-csv.zip

![](https://i.imgur.com/QBXM4Lb.png)

14. 使用jupyter訓練模型

訓練碼截斷

```python=
import mlflow
import mlflow.keras
from mlflow.models.signature import infer_signature

model = Sequential()
model.add(Conv2D(64, kernel_size=(3, 3), activation='relu', input_shape=input_shape))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Conv2D(64, kernel_size=(3, 3), activation='relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Dropout(0.25))
model.add(Flatten())
model.add(Dense(128, activation='relu'))
model.add(Dense(num_classes, activation='softmax'))

model.compile(loss=keras.losses.categorical_crossentropy,
              optimizer=keras.optimizers.Adadelta(),
              metrics=['accuracy'])

model.fit(x_train, y_train,
          batch_size=batch_size,
          epochs=epochs,
          verbose=1,
          validation_data=(x_test, y_test))



score = model.evaluate(x_test, y_test, verbose=0)

# Set an experiment name, which must be unique and case sensitive.

# 填入實驗名稱, 務必符合在mlflow頁面裡的實驗名稱

# 根據填入的實驗名稱會將訓練完的物件儲存在該實驗所設定的儲存貯體(Bucket)

# 例: mnist

mlflow.set_experiment("mnist")

mlflow.start_run()

mlflow.log_metric("cross_entropy_test_loss", score[0])
mlflow.log_metric("test_accuracy", score[1])
print('Test loss:', score[0])
print('Test accuracy:', score[1])
signature = infer_signature(x_test, model.predict(x_test))
input_example = np.array(train_imgs[0].reshape((1,28,28,1)), dtype=np.uint8)

# 對應參數說明

# 1.訓練完的模型: model

# 2.Artifact的相對路徑: artifact_path="keras-model"

# 3.註冊模型的名稱: registered_model_name="MNIST手寫辨識"

# 4.輸入輸出說明: signature=signature

# 5.輸入範例: input_example=input_example

# 務必!填入相對應的參數資料

mlflow.keras.log_model(
model, 
artifact_path="keras-model",
registered_model_name="MNIST手寫辨識",
signature=signature, 
input_example=input_example)

mlflow.end_run()
```

程式碼解釋:

* 設定實驗名稱:

務必符合在mlflow頁面裡的實驗名稱,根據填入的實驗名稱會將訓練完的物件儲存在該實驗所設定的儲存貯體(Bucket)。

```
mlflow.set_experiment("mnist")
```
* 紀錄訓練完的結果

對應參數說明

1.訓練完的模型: model

2.Artifact的相對路徑: artifact_path="keras-model"

3.註冊模型的名稱: registered_model_name="MNIST手寫辨識"

4.輸入輸出說明: signature=signature

5.輸入範例: input_example=input_example

務必填入相對應的參數資料

```
mlflow.keras.log_model(
model, 
artifact_path="keras-model",
registered_model_name="MNIST手寫辨識",
signature=signature, 
input_example=input_example)
```

15. 訓練完成後回到mlflow頁面

* 點擊相對應**實驗**名稱查看訓練結果

例: Experiment: mnist

![](https://i.imgur.com/Ci1wSlK.png)

訓練結果完整資訊

![](https://i.imgur.com/wRZJFuu.png)


* 點擊相對應**註冊模型**名稱查看最新版本的訓練模型

例: 註冊模型: MNIST手寫辨識

![](https://i.imgur.com/5iy0psI.png)

16. 前往**儲存物件管理**, 點擊該實驗所對應的**儲存貯體**(Bucket)

例: Bucket: mlflow-mnist-trained

確認訓練完的物件確實儲存於儲存貯體

![](https://i.imgur.com/M6eQbeM.png)

17. 前往**模型管理**的訓練模型, 點擊測試

![](https://i.imgur.com/0pvNqxF.png)

開啟模型API

![](https://i.imgur.com/waAx1qp.png)

測試模型API

![](https://i.imgur.com/16worzx.png)

18. 測試完成後, 點擊**上架**模型

輸入上架模型名稱,描述和開發團隊

選擇類別,應用領域和建議規格

![](https://i.imgur.com/jxRZt6L.png)


19. 上架完成後, 前往**上架模型**頁面

預設: No Check

等候管理員檢查上架的模型

![](https://i.imgur.com/mU9V9fc.png)

管理員批准的模型

![](https://i.imgur.com/4NMZAEs.png)


20. 前往**模型列表**查看所有批准的模型

![](https://i.imgur.com/VAHeQD6.png)

![](https://i.imgur.com/AWESLRq.png)
 
 
 ---
[Owen's Document](https://hackmd.io/msArbNoVTQ-dgIUqVCEXLw?view)
###### tags: `AIM`
---
> [YPCloud Inc.](https://www.ypcloud.com)
> [name=Owen]
> [time=Oct19, 2021]
