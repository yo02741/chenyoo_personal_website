---
title: 提醒這種小事情交給 Line Notify
date: 2023-03-12 23:00:06
tags:
---

<br />

> 透過 **Line Notify** ∙ **Python** ∙ **Crontab** 實現行動助理

- 運用 `Line Notify` 來達到通知的需求
- 使用 `Python` 作為開發語言
- 使用 `Crontab` 達成排程執行

---

## 發行 Line Notify 權杖
> [Line Notify](https://notify-bot.line.me) > 登入後右上角 > 個人頁面 > 滑到最底下的 `發行存取權杖（開發人員用）`
> 
> 點擊 『 發行權杖 』

<br />

![](https://i.imgur.com/b0LJkSf.png)

## 設定 Line Notify 權杖
> 輸入權杖名稱 > 選擇接收通知的聊天室 > 發行

![](https://i.imgur.com/saIfpGn.png)

<br />

> 複製好 Token 並關閉

![](https://i.imgur.com/RVzdsmK.png)

<br />

> 可以發現已連動的服務多了剛剛設定的 `TEST !!`

![](https://i.imgur.com/AJP9kiO.png)

<br />

## 撰寫 Python Script
> 安裝 Python

> 安裝 requests

> 寫 Python ! 

```python
import requests

def line_notify_message(token, msg):
    headers = {
        'Authorization': 'Bearer ' + token,
        'content-Type': 'application/x-www-form-urlencoded'
    }

    payload = {'message': msg}
    r = requests.post('https://notify-api.line.me/api/notify', headers=headers, params=payload)
    return r.status_code



if __name__ == "__main__":
    # 這邊放 Token
    token = 'HERE IS YOUR TOKEN'
    # 這邊輸入顯示的內容
    message = '\n 你好呀 \n 我是 Line Notify \n 123 !'
    line_notify_message(token, message)
```

<br />

## 執行 / 測試 script
> run 看看這個 script 看看效果

![](https://i.imgur.com/v7AqxCU.png)

<br />

## 透過 Crontab 設定排程

> 撰寫排程
```bash
crontab -e
```


> 開啟編輯器後輸入以下語法：
```bash
*/1 * * * * /Library/Frameworks/Python.framework/Versions/3.11/bin/python3 /Users/yochen/Code/Python/TEST_PYTHON/LineNotify.py
```


分 時 日 月 週 執行語法 執行檔案
以上語法代表我要在無時無刻，每一分鐘，透過 Python 執行我指定的 Python 檔



> 編輯成功後，檢視排程
```bash
crontab -l
```


補充：
- vi 操作：( i 改為 Insert Mode，ESC 後 :wq 儲存退出，[點我](https://dywang.csie.cyut.edu.tw/dywang/linuxSystem/node50.html)看更詳細教學 )
- 尋找本機 Python 安裝連結： `which python3`

<br />


> 靜待時間到來，就可以發現 ～～ 搞定嚕！

![](https://i.imgur.com/oipivCi.png)

---

### 參考文章：
- [Day 8 : LINE Notify 訊息推播通知 (Python版)](https://ithelp.ithome.com.tw/articles/10234115)
- [鳥哥私房菜 - 第十五章、例行性工作排程(crontab)](https://linux.vbird.org/linux_basic/centos7/0430cron.php)