# X / Twitter 批量移除粉丝  
# X / Twitter Bulk Remove Followers

原仓库：
https://github.com/nikolaydubina/twitter-remover

为什么不直接复刻原仓库？

因为我不太会使用 GitHub，截图的时候多次修改 README，不小心暴露了隐私。后来发现修改提交记录也不会弄，所以干脆自己新建一个仓库。

又不是造火箭，能用就行。

---

# 中文说明 🇨🇳

## 功能介绍

这是一个用于 **X（Twitter）批量移除粉丝** 的浏览器控制台脚本。

> 我只有「批量移除粉丝」这个功能需求，所以其他功能没有测试。

复刻时间：

2026年07月08日 01:49:38

---

## 使用方法

### 1. 打开你的粉丝列表

进入：

https://x.com/你的用户名/followers

例如：

https://x.com/xxxxxxxxxxx/followers

其中：

`xxxxxxxxxxx`

替换成你自己的 X 用户名。

---

### 2. 打开浏览器开发者工具

按：

```

F12

```

打开开发者工具。

然后进入：

```

Console（控制台）

```

---

### 3. 允许粘贴

点击控制台最下面输入区域。

手动输入：

```

允许粘贴

````

注意：

⚠️ **不要复制「允许粘贴」这四个字。**

必须自己手动输入。

---

### 4. 运行脚本

复制下面代码，粘贴到 Console 中，然后回车运行。

代码来源：

- 上游仓库复刻版本
- 部分修复来自 ChatGPT 官方免费网页版

如果无法使用，可以尝试让 AI 根据 X 当前页面结构重新修复。

---

## 截图

<img width="1712" height="814" alt="QQ20260708-015542" src="https://github.com/user-attachments/assets/5436e7af-f357-4ae0-97ab-bdc1d518d10f" />


---



## Script

```javascript
let running = true;
let processed = new Set();

async function sleep(ms) {
    return new Promise(r => setTimeout(r, ms));
}

async function removeFollowers() {

    while (running) {

        let users = [...document.querySelectorAll('[data-testid="UserCell"]')];

        let target = users.find(u => {
            let more = u.querySelector('button[aria-label="更多"]');
            return more && !processed.has(more);
        });


        if (!target) {
            window.scrollBy(0, window.innerHeight * 0.7);
            await sleep(2000);
            continue;
        }


        let more = target.querySelector('button[aria-label="更多"]');

        // 标记这个按钮已经处理
        processed.add(more);


        more.click();

        await sleep(800);


        let remove = document.querySelector('[data-testid="removeFollower"]');

        if (remove) {
            remove.click();
        }


        await sleep(800);


        let confirm = document.querySelector('[data-testid="confirmationSheetConfirm"]');

        if (confirm) {
            confirm.click();
        }


        await sleep(1500);
    }
}

removeFollowers();
````

---

# English 🇺🇸

## Introduction

This is a browser console script for **bulk removing followers on X (Twitter)**.

> I only needed the "bulk remove followers" feature, so other features have not been tested.

Original repository:

[https://github.com/nikolaydubina/twitter-remover](https://github.com/nikolaydubina/twitter-remover)

---

## Why not directly fork the original repository?

Because I am not very familiar with GitHub.

While editing screenshots and README files, I accidentally exposed some private information multiple times. I also did not know how to properly remove previous commits.

So I decided to create a new repository instead.

It's not rocket science. If it works, it works.

---

## Fork Time

```
2026-07-08 01:49:38
```

---

## How to Use

### 1. Open your followers page

Go to:

```
https://x.com/your_username/followers
```

Example:

```
https://x.com/xxxxxxxxxxx/followers
```

Replace:

```
xxxxxxxxxxx
```

with your own X username.

---

### 2. Open Developer Tools

Press:

```
F12
```

Open Developer Tools.

Then select:

```
Console
```

---

### 3. Enable Paste

Click the input area at the bottom of Console.

Type manually:

```
允许粘贴
```

Important:

⚠️ **Do not copy and paste the words "允许粘贴".**

You must type them manually.

---

### 4. Run the Script

Copy the script above, paste it into Console, and press Enter.

Source:

* Forked from the upstream repository
* Some fixes were assisted by ChatGPT official free web version

If it stops working, ask an AI to update the script according to the latest X page structure.

---

## Screenshot

<img width="1712" height="814" alt="QQ20260708-015542" src="https://github.com/user-attachments/assets/5436e7af-f357-4ae0-97ab-bdc1d518d10f" />

---

## Script

```javascript
let running = true;
let processed = new Set();

async function sleep(ms) {
    return new Promise(r => setTimeout(r, ms));
}

async function removeFollowers() {

    while (running) {

        let users = [...document.querySelectorAll('[data-testid="UserCell"]')];

        let target = users.find(u => {
            let more = u.querySelector('button[aria-label="更多"]');
            return more && !processed.has(more);
        });


        if (!target) {
            window.scrollBy(0, window.innerHeight * 0.7);
            await sleep(2000);
            continue;
        }


        let more = target.querySelector('button[aria-label="更多"]');

        processed.add(more);

        more.click();

        await sleep(800);

        let remove = document.querySelector('[data-testid="removeFollower"]');

        if (remove) {
            remove.click();
        }

        await sleep(800);

        let confirm = document.querySelector('[data-testid="confirmationSheetConfirm"]');

        if (confirm) {
            confirm.click();
        }

        await sleep(1500);
    }
}

removeFollowers();
```

```
```
