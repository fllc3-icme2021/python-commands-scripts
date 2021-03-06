# Record Commands & Scripts
This repository aims to record some frequently-used commands, including Linux and python commands & archive some frequently-used python scripts.


# Linux Common Command
    cd - 返回上次的目录
  
## 从YouTube下载视频
    !pip3 install youtube-dl ffmpeg-python

    source_url = 'https://www.youtube.com/watch?v=5-s3ANu4eMs' #@param {type:"string"}
    
    # (start, end) 剪取指定时长
    source_start = '00:01:40' #@param {type:"string"}
    source_end = '00:01:50' #@param {type:"string"}

    !mkdir -p /content/data
    !rm -dr /content/data/source*
    !youtube-dl $source_url --merge-output-format mp4 -o /content/data/source_tmp.mp4
    !ffmpeg -y -i /content/data/source_tmp.mp4 -ss $source_start -to $source_end -r 25 /content/data/source.mp4
    !rm /content/data/source_tmp.mp4
   
Taylor Swift videos:

    source_url = 'https://www.youtube.com/watch?v=JgkCFCOAn48'
    source_start = '00:00:08' #@param {type:"string"}
    source_end = '00:00:25' #@param {type:"string"}
    


## 从Linux服务器下载文件到Windows：
    # scp root@10.1.22.5:/root/1.txt e:\scpdata\
    scp xiangmingcan@10.207.174.24:/export2/xiangmingcan/celeba.tar e:    # 下载到E盘
windows上传文件夹到linux服务器：

    scp -rp e:\scpdata root@10.1.22.5:/root
    
Linux服务器之间传输：[点此](https://kernel.blog.csdn.net/article/details/51673229?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.channel_param)

### 远程到本地
以admin的身份把IP地址为“192.168.219.125”，/home/admin/test目录下所有的东西都拷贝到本机/home/admin/目录下
    
    scp -r 用户名@计算机IP或者计算机名称:目录名 本地路径
    scp -r  admin@192.168.219.125:/home/admin/test     /home/admin/
### 本地到远程
    
    scp -r 要传的本地目录名     用户名@计算机IP或名称:远程路径
    scp -r /home/music/    root@ipAddress:/home/root/others/ 
    
### 传输多个文件夹
    scp -r root@192.168.1.104:/usr/local/nginx/html/webs/\{index,json\} ./

    
## linux tar (打包.压缩.解压缩)命令说明 | tar如何解压文件到指定的目录？

    # 不需要加密/或Windows下一步解压，就用这个
    tar -cvf ***.tar /source
    tar -xvf ***.tar
压缩
    
    tar -czvf *name*.tar.gz /source
    tar -cjvf *name*.tar.bz2 /source
    
    tar -czvf 3000.tar.gz 3000/   #举例
解压缩

    tar -xzvf ***.tar.gz
    tar -xjvf ***.tar.bz2
参数解析

    -c: compress建立压缩档案
    -x：解压
    -t：tex 查看内容
    -v: view 查看过程
    -f: force 参数-f是必须的。使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。
    
    -z：有gzip属性的
    -j：有bz2属性的




# Git Command

## download：
    git clone https://github.com/MitchellX/testImage.git
    
无用的：
    mkdir yourFileName
    cd /yourFileName
    git init

## upload：
    git add .        （注：别忘记后面的.，此操作是把Test文件夹下面的文件都添加进来
    git commit  -m  "提交信息"  （注：“提交信息”里面换成你需要，如“first commit”）
    git push -u origin master   （注：此操作目的是把本地仓库push到github上面，此步骤需要你输入帐号和密码）
    ## 一条指令完成
    git add . && git commit -m "update" && git push

## update--(git强制覆盖)：
    git fetch --all
    git reset --hard origin/main
    git pull
    
然后有两种方法来把你的代码和远程仓库中的代码合并

-a. git pull这样就直接把你本地仓库中的代码进行更新但问题是可能会有冲突(conflicts)，个人不推荐

-b. 先git fetch origin（把远程仓库中origin最新代码取回），再git merge origin/master（把本地代码和已取得的远程仓库最新代码合并），如果你的改动和远程仓库中最新代码有冲突，会提示，再去一个一个解决冲突，最后再从1开始

如果没有冲突，git push origin master，把你的改动推送到远程仓库中

## delete:
    git reset --hard HEAD^ 可以将本地的仓库回滚到上一次提交时的状态，HEAD^指的是上一次提交。

# git强制覆盖本地命令（单条执行）：

    git fetch --all && git reset --hard origin/main && git pull


 git 删除远程分支上的某次提交
    git revert HEAD
    git push origin master
    删除最后一次提交，但是查看git log 会有记录
    




   
## 前后台切换命令
https://blog.csdn.net/u011630575/article/details/48288663

    fg          回到上一个进程
    bg          将一个在后台暂停的命令，变成继续执行。如果后台中有多个命令，可以用bg %jobnumber将选中的命令调出
    jobs -l     查看当前所有进程，并显示pid
    kill pid    杀死pid进程
    
## 监控GPU使用情况
    gpustat     最简单的
    watch -n 0.1 nvidia-smi   实时监控 -n设置间隔
    
## 释放GPU一直占用的显存
    fuser -v /dev/nvidia*   查看当前系统中GPU占用的线程
    nvidia-smi              也能查看pid
    kill -9 pid             结束进程
## pytorch查看tensor大小
    import sys
    sys.getsizeof(input.storage())      单位byte B
    
## pytorch查看Net model详情
    print('model.__len__(): %d layers' % model.__len__())
    print(f'model.__len__(): {model.__len__()} layers')

    # U-net(5, 64) memory usage
    param_count = sum(p.storage().size() for p in model.parameters())
    param_size = sum(p.storage().size() * p.storage().element_size() for p in model.parameters())
    param_scale = 2  # param + grad

    print(f'# of Model Parameters: {param_count:,}')
    print(f'Total Model Parameter Memory: {param_size * param_scale:,} Bytes')
    
## View继承nn.Module，这样即可放入nn.Sequential()中了
在接入全连接层前，一般都需要一个打平的操作放在nn.Sequential里面，因此需要自己写一个打平的类继承自nn.Module.以上便是代码，特记录之。

    class View(nn.Module):
    def __init__(self):
        super(View, self).__init__()
    def forward(self, x):
        return x.view(x.size[0], -1)
        
## Conda环境复制的方法
前提是，在本地的conda里已经有一个叫AAA的环境，我想创建一个新环境跟它一模一样的叫BBB，那么这样一句就搞定了：
    
    conda create -n BBB --clone AAA
    conda create -n your_env_name python=X.X（2.7、3.6等)   # Conda 创建虚拟环境
    conda remove -n your_env_name(虚拟环境名称) --all       #  删除虚拟环境
但是如果是跨计算机呢。查询conda create命令的原来说明，是这样的：

    –clone ENV
    Path to (or name of) existing local environment.    
–clone这个参数后面的不仅可以是环境的名字，也可以是环境的路径。所以，很自然地，我们可以把原来电脑上目标conda环境的目录复制到新电脑上，然后再用：

    conda create -n BBB --clone ~/path
参考：https://blog.csdn.net/qq_38262728/article/details/88744268





# 2020-10-22 开始记录京东的笔记


## make cmake 装完包记得 更新一下
    sudo make install

## sudo apt-get install 包之前记得更新源
    sudo apt-get update


## 改变环境变量。要立即生效的话，记得source ~/.bashrc
    export PYTHONPATH=$PYTHONPATH:~/你的环境位置
    export PYTHONPATH=$PYTHONPATH:/home/xiangmingcan/notespace/deepfakes/faceswapNirkin/face_swap/interfaces/python

## 从YouTube下载视频
    !pip3 install youtube-dl ffmpeg-python

    source_url = 'https://www.youtube.com/watch?v=5-s3ANu4eMs' #@param {type:"string"}
    
    # (start, end) 剪取指定时长
    source_start = '00:01:40' #@param {type:"string"}
    source_end = '00:01:50' #@param {type:"string"}

    !mkdir -p /content/data
    !rm -dr /content/data/source*
    !youtube-dl $source_url --merge-output-format mp4 -o /content/data/source_tmp.mp4
    !ffmpeg -y -i /content/data/source_tmp.mp4 -ss $source_start -to $source_end -r 25 /content/data/source.mp4
    !rm /content/data/source_tmp.mp4
   
Taylor Swift videos:

    source_url = 'https://www.youtube.com/watch?v=JgkCFCOAn48'
    source_start = '00:00:08' #@param {type:"string"}
    source_end = '00:00:25' #@param {type:"string"}

# 在终端执行程序时指定GPU

    CUDA_VISIBLE_DEVICES=1 python xxx.py ...
    
    CUDA_VISIBLE_DEVICES=0    python  your_file.py  # 指定GPU集群中第一块GPU使用,其他的屏蔽掉

    CUDA_VISIBLE_DEVICES=1           Only device 1 will be seen
    CUDA_VISIBLE_DEVICES=0,1         Devices 0 and 1 will be visible


    

## 正则表达式
*  匹配 0 或多个字符

?  匹配任意一个字符
   
    mv *.* ./1000/
    mv 6???.* ./6000/
    
## pip install xxx 太慢
    pip install xxx -i https://pypi.tuna.tsinghua.edu.cn/simple
    
### 使用ipdb调试
    python -m ipdb your_code.py


## du查看目录大小，df查看磁盘使用情况。
    df -lh
    du -lh
    
## screen 命令详解
    yum install -y screen	    安装screen工具。
    screen	                  打开一个screen会话
    screen -S <name>          建立一个screen会话，名字是:name
    先按Ctrl+a，再按d	        退出screen会话。
    screen -ls	              查看打开的screen会话。
    screen -r 编号	          退出后再次登录某个会话。
    Ctrl+d或exit	             结束screen会话。
    
    # 强制结束一些，你结束不了的session
    screen -X -S [session # you want to kill] quit



# shell命令
    for i in `ls templates/*.mp4`;do
    name=`basename $i .mp4`
    if [ ! -d templates/$name ];then
    python image2video_fp.py templates/$i templates/$name
    fi
    python main.py $name
    python image2video_fp.py results/${name}_sijiali results/${name}_sijiali.mp4 25
    echo $i
    done
    
basename是指去掉 .mp4后的base名词

#如果文件夹不存在，创建文件夹

    if [ ! -d "/myfolder" ]; then
      mkdir /myfolder
    fi

## shell去掉后缀了前面的路径都可以用basename
    username=$(basename $username) 去掉前置路径
    username=$(basename $username .jpg) 增加去掉后缀


## splitext去掉后缀，basename去掉前置路径，python
    os.path.splitext()[0]
    os.path.basename()
    # 两个连用，只剩名词
    target_name = os.path.splitext(os.path.basename(target_path))[0]
    
### os.path.split()分割文件和上级目录
    landmark_txt = os.path.split(image_path)[1][:-3] + 'txt'
    upper_folder = os.path.split(os.path.split(image_path)[0])[0]
    
### str.split('-', 1 );  以'-'为分隔符，分隔成两个，避免出现多个'-'的情况

### str.rsplit('-', 1), 从后外前开始分割，用法和上面的一致
    
    
# JD Jupyter
    打开ssh端口     bash ~/notespace/xmc
    更新软件源       sudo apt-get update
    激活虚拟环境      source ~/envs/digitalman/bin/activate
    卸载并重装dlib       pip3 uninstall dlib     pip3 install dlib
    设置root密码        sudo passwd
    
### linux下修改python的默认版本：即python2->python3
删除原有链接

    rm /usr/bin/python 

建立新链接

    ln -s /usr/bin/python3.6这是你想要指向的版本号 /usr/bin/python
    
## 想更新最新版软件

    /etc/apt/sources.list

先备份jd的源，然后更新清华源：

    cp sources.list sources.list2
    vim sources.list
    
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
    
更新源千万不能加sudo，不然会失败的！！！
    
    apt-get update
    完成之后，即可装最新的软件了
    
之后想从清华源下载的话，就用-i 指定路径：
    
    pip install virtualenv -i https://pypi.tuna.tsinghua.edu.cn/simple
    
    
    
## 生成文件夹树形目录

windows下的CMD命令tree可以很方便的得到文件夹目录树

    tree /f>list.txt
    
    
## glob.glob(*) 类似正则表达式一样的，找寻目录
    a = glob.glob('*')
    print(a)
    :: ['Audio', 'batch_run.py', 'Data', 'Deep3DFaceReconstruction', 'pipeline.jpg', 'readme.md', 'render-to-video', 'requirements.txt', 'requirements_colab.txt', 'test.py']
    
    
    
## ls 查看文件数量
    ls | wc -l
    
## Windows下编辑的shell脚本在Linux下报错syntax错误
这是编码格式ff（fileformat）的问题，vim进去按照下面指令修改文件格式即可
    
    :set ff=unix
    
## pytorch的Tensor转成int or float
    tensor1.item()
    如何要转成字符串形式：
    str(tensor1.item())
    
## 把tensor多加一个维度
以numpy读入的图片（3, 256, 256） -> (1, 3, 256,256)为例

    img2 = torch.from_numpy(img2).float().unsqueeze(0).cuda()
    
## 用Python将list中的string转换为int
    results = list(map(int, results))
    还能将字符串后面的转义字符'\n \t'去除
    
    
## 将[1, 2 ,3] 转换成string并且作为文件的写入参数
    a = [1, 2, 3]
    log.write(' '.join(map(str, a)))

    
## Python, Numpy求 list 数组均值，方差，标准差
    arr_mean = np.mean(array) 求均值
    # 求按列求均值，只剩一行。axis=1时候，按照行取均值，只剩一列
    arr_mean = np.mean(array, axis=0) 
    arr_var = np.var(array)求方差
    arr_std = np.std(array,ddof=1)求标准差



### 计算欧氏距离Euclidean distance

    dist = np.linalg.norm(vec1-vec2)
    distance= np.sqrt(np.sum(np.square(vec1-vec2)))

### pip 导出当前环境的所有包
    
    pip freeze > ./requirements.txt
    
### linux下解压7z
    sudo apt-get install p7zip-full
    7za x filename.7z

### python 添加上级/下级目录到finding path中
    sys.path.append('..')   # 添加上级目录
    sys.path.append('code/')   # 添加下级code/目录

    
### cv2在图片中添加文字
    # 各参数依次是：照片/添加的文字/左上角坐标/字体/字体大小/颜色/字体粗细
    cv2.putText(I,'there 0 error(s):',(50,150),cv2.FONT_HERSHEY_COMPLEX,6,(0,0,255),25)
    
### cv2.imread()读取通道顺序，以及转换颜色通道
    img = cv2.imread(fengmian)
    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) # cv2默认为bgr顺序
    h, w, _ = img.shape #返回height，width，以及通道数，不用所以省略掉
    
### cv2如果要读取4通道的rgba数据，要加-1表示读到最后一位，不然的话平常只会读前三维
    cv2.imread(img, -1)
    
### cv2裁剪坐标
    cropped = img[0:128, 0:512]  # 裁剪坐标为[y0:y1, x0:x1]，先width后height
    
### cv2图片简单拼接 hconcat vconcat函数使用
    img =cv2.imread(file_path[i])
    img=cv2.hconcat([img,img,img])#水平拼接
    img=cv2.vconcat([img,img,img])#垂直拼接
    
### cv2用np.concatenate去拼接图片
    np.concatenate((img, img, img), axis=1) 
    axis=0表示只剩一列，axis=1表示只剩一行，注意这里！里面是括号，tuple元组的形式
    
### cv2获取图像的三通道，并且写视频cv2.VideoWriter()
    fourcc = cv2.VideoWriter_fourcc(*'MJPG')
    w, h, c = test_img.shape
    video_writer = cv2.VideoWriter(save_name, fourcc, fps, (h, w))
    
    for img in imgs:
        if img[-3:] != 'jpg' and img[-3:] != 'png':
            continue
        imgname = os.path.join(imgs_dir, img)
        frame = cv2.imread(imgname, -1)
        video_writer.write(frame)

    video_writer.release()

### python调用shell命令
    import os
    os.system("cmd")
    
    
### Python 随机数生成
    import random
    x = random.randint(0,9)
    
