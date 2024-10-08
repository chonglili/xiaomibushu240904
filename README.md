# 小米运动自动刷步数

> 小米运动自动刷步数

## Github Actions 部署指南

### 一、Fork 此仓库

### 二、设置账号密码

添加名为 **USER**、**PWD**、**STEP** 的变量，值分别为 **账号（仅支持手机号）**、**密码**、**步数（0则为18000-25000之间随机 或自定义随机范围[18000-25000]）**

> settings> secrets and variables> secrets> actions Repository secrets



### 三、多账户(用不上请忽略)

多账户请用 **#** 分割 然后保存到变量 **USER** 和 **PWD**

#### 例如

**13800138000#13800138001** 变量 **USER**

**abc123qwe#abcqwe2** 变量 **PWD**

### 四、自定义启动时间

编辑 **.github/workflows/run.yml**

找到 cron: 0 10 * * *

修改其中的10为你需要修改的时间

需要运行的时间-8就是UTC时间，比如上午9点，9-8=1，则cron: 0 1 * * *

### 240909 添加自定义步数变量，STEP1 STEP2 STEP3,进行步数增加，从而在不同的run1.yml ruan2.yml...中采用不同的step1 step2,实现步数的增加


### 五、启动

> Actions-->点击“I understand my workflows, go ahead and enable them”-->All workflows-->刷步数-->点击“Enable workflow”

## 注意事项

1. 每天运行一次，在下午 6 点

2. 多账户的数量和密码请一定要对上 不然无法使用!!!

3. 启动时间得是UTC时间!

4. 如果支付宝没有更新步数,到小米运动->设置->账号->注销账号->清空数据,然后重新登录,重新绑定第三方

5. 更新了获取时间戳的方式为本地获取，淘宝的很多时候连不上
    把原文的t=get_time()  变为get_timestamp()，并把时间戳换成下边这个即可
   改：# 13位时间戳
    def get_timestamp():
    return str(int(time.time() * 1000))
   或修改为调用北京时间并改为毫秒级时间戳
   def get_time():
    current_time = get_beijing_time()
    return "%.0f" % (current_time.timestamp() * 1000)

