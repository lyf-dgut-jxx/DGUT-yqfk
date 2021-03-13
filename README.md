本Repo仅修改为可自用版本，不保证脚本能正常运行
如有疑问请访问元Repo
## Usage

```
USERNAME   # 学号
PASSWORD   # 中央认证系统密码
SCKEY      # Server 酱密钥
```

[Server 酱密钥获取](http://sc.ftqq.com/)

//本Repo移除了APScheduler


### 使用 (Actions) 【推荐】

请先在Settings>>Secrect 添加USERNAME,USERPASSWD,SCKEY三个Actions secrets

```shell script
name: DGUT_yqfk

on:
    workflow_dispatch:
    schedule:
        - cron: "10 */2  *  *  *"
    watch:
        types: [started]


jobs:
  build:
    runs-on: ubuntu-latest
    steps:
            - name: Checkout
              uses: actions/checkout@v2
        
            - name: "Set up Python"
              uses: actions/setup-python@v1
              with:
                python-version: 3.8

            - name: "requirements"
              run: pip3 install -r requirements.txt

            - name: "Run yqfk"
              env:
                USERNAME: ${{ secrets.USERNAME }}
                PASSWORD: ${{ secrets.USERPASSWD }}
                SCKEY: ${{ secrets.SCKEY }}
              run: 
                python yqfk.py
```
