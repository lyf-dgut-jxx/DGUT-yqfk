本Repo仅修改为可自用版本，不保证脚本能正常运行
如有疑问请访问元Repo
## Usage

```
USERNAME   # 学号
PASSWORD   # 中央认证系统密码
SCKEY      # Server 酱密钥
```

[Server 酱密钥获取](http://sc.ftqq.com/)

默认在 00:10 的时候提交（不一定工作

### 方法一 (docker-compose)

```yaml
version: "3.1"

services:
  yqfk:
    image: ssrinke/yqfk
    environment:
      - USERNAME=
      - PASSWORD=
      - SCKEY=
    restart: always
```

### 方法二 (screen)

可以使用`screen`将程序放置在后台运行(Ctrl + A + D 离开 screen)

```shell script
git clone https://github.com/Rinbili/DGUT-yqfk.git && cd DGUT-yqfk 
pip3 install -r requirements.txt
screen -US yqfk
python3 yqfk.py USERNAME PASSWORD SCKEY
```

### 方法三 (Actions) 【推荐】

先在Settings>>Secrect 添加USERNAME,USERPASSWD,SCKEY三个Actions secrets

```shell script
name: DGUT_yqfk

on:
    workflow_dispatch:
    schedule:
        - cron: "10 0,1,2,3  *  *  *"
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
