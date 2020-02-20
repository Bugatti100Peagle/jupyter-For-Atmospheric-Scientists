# jupyter For Atmospheric Scientists

## 介绍

 Jupyterlab 镜像预装 Python3，C，Fortan，Grads，Julia，R内核，Metpy，Siphon，atmos，basemap，ncl_to_Python，Cartopy，ecmwf-api，netcdf等常用包。

Docker images of Jupyterlab with Python3, C, Fortan, Grads, Julia, R and Metpy, Siphon, atmos, basemap, ncl_to_Python, Cartopy, ecmwf-api.

## 使用截图

| ![https://img.bugatii100peagle.cn/2020/02/18/44d5d10d73152.png](https://img.bugatii100peagle.cn/2020/02/18/44d5d10d73152.png) | ![https://img.bugatii100peagle.cn/2020/02/18/362d47fcfb311.png](https://img.bugatii100peagle.cn/2020/02/18/362d47fcfb311.png)  |
| ------------ | ------------- |
| ![https://img.bugatii100peagle.cn/2020/02/18/36c7dd118359b.png](https://img.bugatii100peagle.cn/2020/02/18/36c7dd118359b.png) | ![https://img.bugatii100peagle.cn/2020/02/18/ec9bbcf04edf9.png](https://img.bugatii100peagle.cn/2020/02/18/ec9bbcf04edf9.png)|

无需复杂设置与安装，开包即用。（PS：尤其是Basemap，简直是气象人的噩梦）

## 安装教程

服务器要求，至少1 vCPU 2 GiB，已配置网络环境，安全组开放`8000`端口。（也可以是其他端口，注意修改`run`命令即可）

推荐用[宝塔面板](https://www.bt.cn/)安装。

### 1. 下载并安装Docker ce

卸载旧版本Docker

```bash
sudo apt-get remove docker docker-engine docker.io
```

安装包以允许通过HTTPS使用存储库

```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

添加Docker的官方GPG密钥

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

确认指纹

```bash
sudo apt-key fingerprint 0EBFCD88
```

设置稳定存储库，默认最新版

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

再次更新apt包索引

```bash
sudo apt-get update
```

安装最新版本的Docker CE

```bash
sudo apt-get install docker-ce
```

查看Docker CE 版本

```bash
docker -v
```

### 2. 拉取阿里云镜像

已打包七种镜像可供选择，如下：

| 镜像名| 大小 | Python3 C Grads Julia R |Metpy Siphon atmos | basemap | ncl_to_Python | Cartopy | ecmwf-api | netcdf | Fortan |
| ------------ | ------------- | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |
| jupytercgmsabefcn:v1 | 3.001 GB  | √ | √ | √ |   | √ | √ | √ | √ |
| jupytercgrads_metpy_siphon_atmos_nal_ecmwf_fortran:v1 | 2.600 GB | √ | √ |   | √ |   | √ |   | √ |
| jupytercgrads:1 | 1.871 GB | √ |  | |  | |  | |  |
| jupytercgrads_metpy_siphon_atmos:v1 | 1.978 GB | √ | √ | |  | |  | |  |
| jupytercgrads_metpy_siphon_atmos_basemap:v1 | 2.794 GB | √ | √ | √ |  | |  | |  |
| jupytercgrads_metpy_siphon_atmos_basemap_ecmwf_fortran:v1 | 2.794 GB | √ | √ | √ |  |  | √ | | √ |
| jupytercgrads_metpy_siphon_atmos_basemap_ecmwf_fortran_cartopy:v1 | 2.959 GB | √ | √ | √ |  | √ | √ | | √ |

本教程以装有Basemap和netCDF4的jupytercgmsabefcn为例，拉取链接为`docker pull registry.cn-shanghai.aliyuncs.com/bugatii100peagle/镜像名:版本`

```bash
docker pull registry.cn-shanghai.aliyuncs.com/bugatii100peagle/jupytercgmsabefcn:v1
```

### 3. 运行镜像

本地新建文件夹`jupyterlab`，`jupyterlab/workspace`

```bash
docker run --name jupytercgmsabefcn -d -p 8000:8888 -v `pwd`/jupyterlab:/workspace -w /workspace -e GRANT_SUDO=yes --user root registry.cn-shanghai.aliyuncs.com/bugatii100peagle/jupytercgmsabefcn jupyter-lab --no-browser --port=8888 --ip=0.0.0.0 --allow-root
```

## 使用说明

浏览器打开`http://IP:8000`，密码是空密码，直接回车即可。

![https://img.bugatii100peagle.cn/2020/02/20/442292d9a302a.png](https://img.bugatii100peagle.cn/2020/02/20/442292d9a302a.png)

## TODO 接下来要做

- [ ] 1. 国际化本项目文档。
- [ ] 2. 收集更多常用工具集成。
- [ ] 3. 试图解决NCL与Basemap的冲突，设置虚拟环境，集成到一个镜像。
- [ ] 4. 修复低版本Grads无法打开`.nc`文件的问题。

## 参与项目

欢迎下载镜像使用，如果你觉得不错就给个星吧。

如果你有什么需求建议，可以在`issue`中以`需求：xxx`的形式给出。

如果你安装遇到问题，可以在`issue`中以`问题：xxx`的形式给出，并标明宿主机环境，报错信息等。

从裸奔的Jupyter镜像安装的详细方法，可参考我的博文[气象人的Jupyterlab](https://blog.bugatii100peagle.cn/2020/02/17/%E6%B0%94%E8%B1%A1%E4%BA%BA%E7%9A%84JupyterLab/).

## 打赏

|![https://bugatii100peaglepics.oss-cn-qingdao.aliyuncs.com/HexoTheme/img/WX_cr.png](https://bugatii100peaglepics.oss-cn-qingdao.aliyuncs.com/HexoTheme/img/WX_cr.png)| ![https://bugatii100peaglepics.oss-cn-qingdao.aliyuncs.com/HexoTheme/img/ZFB_cr.jpg](https://bugatii100peaglepics.oss-cn-qingdao.aliyuncs.com/HexoTheme/img/ZFB_cr.jpg) |
| ------------ | ------------- |
