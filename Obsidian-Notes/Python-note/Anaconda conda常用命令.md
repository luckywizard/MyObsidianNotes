# Anaconda conda常用命令
## 参考
[Getting started with conda](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html)

## 1. 管理conda自身  
### 1.1 查看conda版本  
```bash
conda --version
```

### 1.2 查看conda的环境配置  
```bash
conda config --show
```

### 1.3 设置国内镜像
- 设置方法如下所示：
```bash
#设置清华镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

#设置搜索时显示通道地址
conda config --set show_channel_urls yes
```

### 1.4 显示安装的频道

```bash
 conda config --set show_channel_urls yes 
```

### 1.5 查看已经添加的channels

```bash
conda config --get channels
```

### 1.6 已添加的channel在哪里查看

```bash
vim ~/.condarc
```

### 1.7 更新conda
- 将conda自身更新到最新版本，it is recommended to always keep conda updated to the latest version.         
```bash
conda update conda
```

- 更新Anaconda整体
将整个Anaconda都更新到确保稳定性和兼容性的最新版本
```bash
conda update Anaconda
```

### 1.8 查询某个命令的帮助 
```bash
conda create --help
```

## 2. 管理环境
Conda允许你创建相互隔离的独立环境，这些环境被称之为虚拟环境（Virtual Environment），这些环境各自包含属于自己的文件、包以及他们的依存关系，并且不会相互干扰。

### 2.1. 创建虚拟环境
- 使用conda创建虚拟环境的命令格式为:
```bash
conda create -n env_name python=3.8
# 这表示创建python版本为3.8、名字为env_name的虚拟环境。
```
     
- 创建虚拟环境的同时安装必要的包
```bash
conda create -n env_name numpy matplotlib python=3.8
```

### 2.2 查看有哪些虚拟环境
```bash
conda env list
conda info -e
conda info --envs
```

###  2.3 激活虚拟环境
```bash
conda activate env_name
# 此时使用python --version可以检查当前python版本是否为所想要的（即虚拟环境的python版本）。
```

### 2.4 退出虚拟环境
```bash
conda activate
conda deactivate
```

### 2.5 删除虚拟环境
- 执行以下命令可以将该指定虚拟环境及其中所安装的包都删除。
```bash
conda remove --name env_name --all
```
       	
- 如果只删除虚拟环境中的某个或者某些包则是：
```bash
conda remove --name env_name  package_name
```

### 2.7 导出环境   
```bash
#获得环境中的所有配置
conda env export --name myenv > myenv.yml
#重新还原环境
conda env create -f  myenv.yml
```

## 3. 包（Package）的管理
### 3.1 查询包的安装情况
- 查询看当前环境中安装了哪些包
```bash
conda list
```

- 查询当前Anaconda repository中是否有你想要安装的包
```bash
conda search <package_name>  #模糊查找,查询到所有的package_name相关字段的包
```

 - 搜索指定的包
```bash
conda search --full-name  <package name>  

# 使用命令 
conda search --full-name tensorflow # 显示所有的tensorflow包。
```

### 3.2 包的安装和更新
- 在当前（虚拟）环境中安装一个包：
```bash
conda install <package_name>
```

- 安装某个特定版本的包(以下例为安装0.20.3版本的numpy)：
```bash
conda install numpy=0.20.3
```

- 更新指定的包
```bash
conda update <package_name>  


conda update numpy
```

- 安装包的时候可以指定从哪个channel进行安装，比如说，以下命令表示不是从缺省通道，而是从conda_forge安装某个包。
```bash
conda install pkg_name -c conda_forge
```

### 3.3 conda卸载包
```bash
conda uninstall package_name  #这样会将依赖于这个包的所有其它包也同时卸载。
```

- 如果不想删除依赖其当前要删除的包的其他包：
```bash
conda uninstall package_name --force  #并不建议用这种方式卸载，因为这样会使得你的环境支离破碎
```

### 3.4 清理anaconda缓存
```bash
conda clean -p      # 删除没有用的包 --packages
conda clean -t      # 删除tar打包 --tarballs
conda clean -y -all # 删除所有的安装包及cache(索引缓存、锁定文件、未使用过的包和tar包)
```

