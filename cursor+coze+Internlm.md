# 一、教程简介

## 

## 


# 二、准备工作

## 1. 注册小程序

点击[微信小程序注册](https://mp.weixin.qq.com/cgi-bin/wx?token=&lang=zh_CN)，注册小程序。

![注册](https://github.com/user-attachments/assets/b4b1ea04-83c8-4e7d-9dba-b0afba7e2009)

页面下拉，进行微信开发者工具下载。

点击[微信开发者工具下载](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)，下载开发者工具并安装。

![下载](https://github.com/user-attachments/assets/7e42faa1-a116-4888-bcc0-23c5b89a8877)

注册完小程序后，想要能发布上线，需要进行基本信息填写、类目认证、微信认证、备案。其中认证费是300元，会有工作人员座机电话核实，这里我就不一一演示了，直接拿已有账号演示。

![发布前工作](https://github.com/user-attachments/assets/e0af0a40-607b-42b2-9e7e-3abff3be0dd8)

## 2. cursor下载安装

点击[cursor官网](https://www.cursor.com/),点击download for free开始下载。

![下载](https://github.com/user-attachments/assets/71cd306b-9fa2-49e6-8d34-ad271bc41d02)


# 三、搭建生成图片工作流

## 1. 调用internlm_api插件

![新建插件](https://github.com/user-attachments/assets/48558309-de2e-4db1-9876-707d24a649f1)

### 1.1 新建插件

![新建1](https://github.com/user-attachments/assets/efab7b00-30cd-4e6c-a7b9-ddd4a5165905)

![新建2](https://github.com/user-attachments/assets/d3a5d555-a5f6-4e63-8541-ce195b396305)

### 1.2 配置元数据

仔细阅读[书生浦语的API文档](https://internlm.intern-ai.org.cn/api/document)。其中模型、请求地址、api_key可以固定，我们设置输入prompt和user_request，输出为answer。

![配置元数据](https://github.com/user-attachments/assets/13cd806e-42c5-472f-b194-a7441316d01d)

### 1.3 代码

首先，我们要先去拿到api_token，[点击](https://internlm.intern-ai.org.cn/api/tokens),新建API TOKEN，保存好我们的token，去替换下面代码里用到的api_key值。

![新建token](https://github.com/user-attachments/assets/df664b99-7c42-4de4-b3b5-b2d3e5e3cbba)

修改第14行的API_KEY 为你自己的api_token。

```
import requests
from typing import TypedDict, Optional

# 入参
class Input(TypedDict):
    prompt: str
    user_request: str

# 输出
class Output(TypedDict):
    answer: str

# 固定的API配置
API_KEY = "" # 固定API密钥
API_URL = "https://internlm-chat.intern-ai.org.cn/puyu/api/v1/chat/completions"  # 固定请求地址

def handler(args) -> Output:
    # 获取输入变量
    prompt = args.input.prompt
    user_request = args.input.user_request

    # 调用merge_prompt函数合并提示词和用户要求
    full_prompt = merge_prompt(prompt, user_request)

    # 调用ask_question函数获取answer
    answer = ask_question(full_prompt)
    return {"answer": answer if answer else ""}

def merge_prompt(prompt: str, user_request: str) -> str:
    """提示词和用户需求拼接处理函数"""
    # 拼接提示词和用户需求
    full_prompt = f'{prompt}, 【用户提供的描述】 - {user_request}'
    return full_prompt

def ask_question(question: str) -> Optional[str]:
    try:
        headers = {
            "Content-Type": "application/json",
            "Authorization": f"Bearer {API_KEY}"
        }

        data = {
            "model": "internlm2.5-latest",
            "messages": [{
                "role": "user",
                "content": question
            }],
            "n": 1,
            "temperature": 0.8,
            "top_p": 0.9
        }
        response = requests.post(API_URL, headers=headers, json=data)
        message = response.json()

        if 'error' not in message:
            return message['choices'][0]['message']['content']
        else:
            print("无法获取模型回答:", message.get('error', 'Unknown error'))
            return None

    except requests.exceptions.RequestException as e:
        print(f"请求错误：{e}")
        return None
    except Exception as e:
        print(f"发生错误: {str(e)}")
        return None
```

### 1.4 测试

测试前，先安装requests安装依赖包。

![安装依赖包](https://github.com/user-attachments/assets/aebe3cb3-8eaf-4164-a57e-9b1d5c286f8a)

先点击“自动生成”，再修改里面的输入，点击运行，测试效果如下图所示：

![测试](https://github.com/user-attachments/assets/0b52b3ef-0869-4a3e-9f52-9234fc7ce404)

### 1.5 发布

每次修改之后都要发布才能给工作流或者Bot调用。

![发布成功](https://github.com/user-attachments/assets/99227429-2442-4183-99cd-1a3b00a81529)

## 2. 搭建生成图片工作流

### 2.1 新建create_imgs工作流

![新建工作流](https://github.com/user-attachments/assets/2595a275-adef-45fc-9706-3f3ccb0a5c99)

### 2.2 添加大模型插件


### 2.3 添加生成图片插件

### 2.4 

