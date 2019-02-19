
## testhexo仓库用来存放由hexo生成的站点源文件以及静态网站资源
Clone with HTTPS：`git clone https://github.com/sudehao/testhexo.git`  
`master`分支存放`public`静态资源  
`hexo`分支存放站点源文件以及文章资源*（设为默认分支）

### 搭建流程
1. ##### 在[GitHub.com](https://github.com/)上创建仓库
创建时，不要勾选初始化  
如果需要使用page功能要选择public
2. #### 拷贝远程仓库到本地：
    ``` BASH
    #  克隆远程仓库并进入 本地仓库文件夹 - testhexo
    git clone https://github.com/sudehao/testhexo.git testhexo && cd testhexo  
    ```

> 以下命令全部在本地仓库目录下执行！！！（本例为：testhexo）

3. #### 创建分支`hexo`：

    ``` BASH
    git checkout -b hexo      # 创建分支hexo，自动设为当前分支
    ```

4. #### 通过`Git bash`执行：
    ``` BASH
    npm install -g hexo-cli   # 安装 hexo
    hexo init aaa      # 初始化一个静态网站`aaa`
    mv aaa/{.,}* ./    # 移动aaa所有文件到 本地仓库文件夹
    rm -rf aaa/        # 删除aaa文件夹
    npm install        # 站点模块包安装，hexo s 开启服务，可以查看效果
    npm install hexo-deployer-git   # 安装 deploy，用于同步public/*到远程仓库
    ```
5. #### 修改站点配置文件_config.yml，对Deploy进行配置：
    ``` YML
    # Deployment
    ## Docs：   https://hexo.io/docs/deployment.html
    ## Docs_CN：https://hexo.io/zh-cn/docs/deployment
    deploy:
    type: git       # 类型
    repo: https://github.com/sudehao/testhexo.git      # 库(Repository)地址
    branch: master  # 分支名称设置为 master。
    message:        # 自定义提交信息 (默认为 Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }})
    ```
6. #### 提交站点源文件到远程仓库hexo分支：
    ``` BASH
    git add .
    git commit -m "..."
    git push origin hexo # 推送站点源文件到hexo分支，hexo自动设置为默认分支
    ```
7. #### 生成站点静态文件并部署到GitHub上：
    ``` BASH
    hexo d # 自动部署网站到远程仓库的master分支
    ```

### 日常更新站点流程
在本地仓库进行修改操作（如：添加新文章、修改样式等）  
通过以下流程推送到远程仓库hexo分支
1. #### 依次执行将改动推送到GitHub（此时当前分支应为hexo）：
    ``` BASH
    git add ./*
    git commit -m "..."
    git push origin hexo
    ################## 命令使用说明 #################
    # git checkout hexo   # 切换到hexo分支
    # git branch -d hexo  # 删除分支hexo
    # git branch          # 查看分支，*号的为当前分支
    # git status          # git本地状态
    ```
2. #### 最后，执行 `hexo d` 推送站点静态文件到远程仓库的master分支
如果出现标签统计错误问题，执行`hexo clean`清理缓存后在执行`hexo d`
### 重装系统或更换电脑后
1. #### 拷贝仓库（默认分支为hexo）：
    ``` BASH
    git clone https://github.com/sudehao/testhexo.git testhexo
    ```
2. #### 在拷贝的本地仓库文件夹下通过`Git bash`依次执行指令：（本例为：testhexo）
    ``` BASH
    npm install -g hexo-cli
    npm install
    npm install hexo-deployer-git
    ```
    记得，不需要`hexo init <folder>`这条指令