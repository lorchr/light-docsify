# Dev Environment

# 1. 软件列表
1. IDEA             zhile.io
2. DBeaver
3. MobaxTerm
4. VS Code
5. Maven            mvnrepository.com
6. JDK
7. Git
8. U Tools
9. Docker
10. Chrome
11. 企业微信\钉钉
12. FoxMail

# 2. 软件安装
## 1. [IDEA](zhile.io)

1. Jrebel

```
GUID生成：https://www.guidgen.com/

激活URL :https://jrebel.qekang.com/GUID

激活成功后设置为离线模式
```

2. MyBatisCodeHelper-Pro

3. Translation - 必备的翻译插件
4. CodeGlance - 缩略图
5. Grep Console - 控制台日志 高亮
6. String Manipulation -对字符串的处理
7. GenerateAllSetter - 自动调用所有 Setter 函数（可填充默认值）
8. Maven Helper - 方便maven项目解决jar冲突
9. RestfulToolkit — 快捷跳转Action方法
10. Free Mybatis Plugin , MybatisX
11. EasyCode
12. EasyYapi
13. GeneratrSerialVersionUID
14. JFormDesigner
15. PlantUML Integration
16. ResourceBundle Editor
17. SonarAnalyzer
18. TestMe
19. UML Generator
20. VisualVM Launcher

21. CamelCase - 多种命名格式之间切换
22. Presentation Assistant - 快捷键展示
23. Key promoter X — 会有这个操作的快捷键在界面的右下角进行告知。
24. Codota — 代码智能提示
25. Alibaba Java Code Guidelines — 阿里巴巴 Java 代码规范
26. Rainbow Brackets — 让你的括号变成不一样的颜色，防止错乱括号
27. HighlightBracketPair — 括号开始结尾 高亮显示。
28. google-java-format — 代码自动格式化
29. Leetcode Editor - 可以在IDEA中在线刷题。
30. Statistic — 项目信息统计
31. jclasslib bytecode viewer - 查看字节码
32. Auto filling Java call arguments - 自动补全参数
33. GenerateO2O — 自动填充参数的值
34. FindBugs — 检查代码中的隐患
35. SonarLint — 检查代码中的隐患
36. SequenceDiagram — 调用链路自动生成时序图
37. Stack trace to UML — 根据 JVM 异常堆栈画 UML时序图和通信图
38. Java Stream Debugger — Stream 将操作步骤可视化
39. IDEA QAPlug - 帮助我们提前找到潜在的问题bug


## 2. Git
```shell

git config --global user.name "lorchr"
git config --global user.email "lorchr@163.com"

ssh-keygen -t rsa -C "lorchr@163.com"
cat /c/Users/lorchr/.ssh/id_rsa.pub

git init
git add .
git commit -m "Init project"
git remote add origin https://cloud.com/lorchr/spring-cloud-samples.git
git branch --set-upstream-to=origin/master master
git push -u origin master
```

常用操作
```shell
-- 克隆仓库
git clone http://github.com/lorchr/spring-cloud-samples.git

-- 查看远程仓库地址
git remote -v

-- 移除远程仓库
git remote rm origin

-- 添加新的远程仓库地址
git remote add           cloud https://gitee.com/lorchr/spring-cloud-samples.git
git remote set-url --add origin http://github.com/lorchr/spring-cloud-samples.git
git push -u cloud master

# 提交
git push 仓库别名 分支 --allow-unrelated-histories
# 检出
git pull 仓库别名 分支 --allow-unrelated-histories
```

## 3. Docker更换软件源

修改Docker容器内部的软件源地址

1. 使用sed替换
    
    ```shell
    # 使用root用户执行命令行操作
    docker exec -it -u root <container-id(name)> /bin/bash

    # 查看软件源
    cat /etc/apt/sources.list

    # 替换软件源
    sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list
    sed -i "s@http://security.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list
    ```

如果使用的https源，则需要执行`apt install apt-transport-https`，再执行`apt update`更新源索引

2. 直接编辑 sources.list

    ```shell
    # 使用root用户执行命令行操作
    docker exec -it -u root <container-id(name)> /bin/bash

    # 查看系统版本
    cat /etc/os-release

    ## 追加
    cat << EOF >> /etc/apt/sources.list
    # Debian 10 buster

    # 中科大源

    deb http://mirrors.ustc.edu.cn/debian buster main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian buster-backports main contrib non-free
    deb http://mirrors.ustc.edu.cn/debian-security/ buster/updates main contrib non-free

    deb-src http://mirrors.ustc.edu.cn/debian buster main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian buster-updates main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian buster-backports main contrib non-free
    deb-src http://mirrors.ustc.edu.cn/debian-security/ buster/updates main contrib non-free

    # 官方源

    # deb http://deb.debian.org/debian buster main contrib non-free
    # deb http://deb.debian.org/debian buster-updates main contrib non-free
    # deb http://deb.debian.org/debian-security/ buster/updates main contrib non-free

    # deb-src http://deb.debian.org/debian buster main contrib non-free
    # deb-src http://deb.debian.org/debian buster-updates main contrib non-free
    # deb-src http://deb.debian.org/debian-security/ buster/updates main contrib non-free

    # 网易源

    # deb http://mirrors.163.com/debian/ buster main non-free contrib
    # deb http://mirrors.163.com/debian/ buster-updates main non-free contrib
    # deb http://mirrors.163.com/debian/ buster-backports main non-free contrib
    # deb http://mirrors.163.com/debian-security/ buster/updates main non-free contrib

    # deb-src http://mirrors.163.com/debian/ buster main non-free contrib
    # deb-src http://mirrors.163.com/debian/ buster-updates main non-free contrib
    # deb-src http://mirrors.163.com/debian/ buster-backports main non-free contrib
    # deb-src http://mirrors.163.com/debian-security/ buster/updates main non-free contrib

    # 阿里云

    # deb http://mirrors.aliyun.com/debian/ buster main non-free contrib
    # deb http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib
    # deb http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib
    # deb http://mirrors.aliyun.com/debian-security buster/updates main

    # deb-src http://mirrors.aliyun.com/debian/ buster main non-free contrib
    # deb-src http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib
    # deb-src http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib
    # deb-src http://mirrors.aliyun.com/debian-security buster/updates main
    EOF
    ```

3. 安装软件
   
   ```shell
    # 更新软件源
    apt-get update && apt-get upgrade -y

    # 安装apt-file
    apt-get install -y apt-file && apt-file update

    # 查找软件
    apt-file search /bin/ps | grep -w "bin/ps"

    # 安装软件
    apt-get install -y vim wget

    # Docker容器交互
    docker exec -it -u root <container-id(name)> /bin/bash
   ```

4. 上传下载文件
   
   ```shell
    # 上传
    docker cp <local_file_path> <container-id(name)>:<container_path>
    docker cp C://users/light/Desktop/elasticsearch-analysis-ik elasticsearch:/usr/share/elasticsearch/plugins/elasticsearch-analysis-ik

    # 下载
    docker cp <container-id(name)>:<container_path> <local_file_path>
    docker cp elasticsearch:/usr/share/elasticsearch/plugins/elasticsearch-analysis-ik C://users/light/Desktop/elasticsearch-analysis-ik
   ```

# 3. Mysql
[Mysql](devenv/Docker-Mysql.md ':include')

# 4. Pgsql
[Pgsql](devenv/Docker-Pgsql.md ':include')

# 5. Redis
[Redis](devenv/Docker-Redis.md ':include')

# 6. InfluxDB
[InfluxDB](devenv/Docker-InfluxDB.md ':include')

# 7. EMQX
[EMQX](devenv/Docker-EMQX.md ':include')

# 8. Elasticsearch
[Elasticsearch](devenv/Docker-Elasticsearch.md ':include')

# 9. Windows下Docker端口被占用的问题
[Docker port bind error in Windows](devenv/Docker-Port-Bind-Error-In-Windows.md ':include')
