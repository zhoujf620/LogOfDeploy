FROM ubuntu:16.04

# 更新源，安装基础依赖库，创建python3.6 环境
ADD sources.list /etc/apt/
RUN apt-get update\
&& apt-get install build-essential -y\
&& apt-get install python-software-properties -y\
&& apt-get install software-properties-common -y\
&& add-apt-repository ppa:jonathonf/python-3.6 -y\
&& apt-get update\
&& apt-get install python3.6 -y\
# && apt-get install python3.6-dev -y\
&& rm /usr/bin/python\
&& ln -s /usr/bin/python3.6 /usr/bin/python\
&& rm /usr/bin/python3\
&& ln -s /usr/bin/python3.6 /usr/bin/python3\
&& apt-get install python3-pip -y\
&& pip3 install pip -U\
&& rm /usr/bin/pip3 \
&& ln -s -f /usr/local/bin/pip3 /usr/bin/pip3\
&& ln -s -f /usr/local/bin/pip3 /usr/bin/pip\
&& pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 安装python依赖库
ADD packages.txt $PATH/packages.txt
RUN pip3 install --upgrade setuptools && pip3 install -r $PATH/packages.txt

# 设置时区
ENV TIME_ZONE=Asia/Shanghai 
RUN ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime\
&& echo $TIME_ZONE > /etc/timezone\
&& apt-get install tzdata\
&& dpkg-reconfigure -f noninteractive tzdata

# 默认暴露端口
EXPOSE 5000

# 复制代码
COPY  ./code/ $PATH/code/
WORKDIR $PATH/code/
# 容器启动命令
CMD python server.py 