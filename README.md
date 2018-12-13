# Harbor-ARM64

   由于目前并未发现Harbor官方对ARM64架构提供支持，出于需要，我使用https://github.com/goharbor/harbor 源码，参考https://github.com/goharbor/harbor/blob/master/docs/compile_guide.md 文档在ARM64设备上进行编译，产生Harbor部署所需镜像以及离线安装包。以下是主要说明：
   
1.编译需要在ARM64架构的设备上进行。

2.docker-compose编译参考：https://github.com/ubiquiti/docker-compose-aarch64 。

3.编译命令：
'''
make package_offline GOBUILDIMAGE=golang:1.9.2 COMPILETAG=compile_golangimage 
'''

4.版本控制
'''
修改Makefile中的参数：
VERSIONTAG :镜像tag
PKGVERSIONTAG :安装包版本
'''

5* 遗留问题：
   在编译tools/migration/时由于photon:3.0-aarch64的tdnf源：https://dl.bintray.com/vmware/photon_release_3.0_aarch64/aarch64/ 缺少mariadb-server mariadb mariadb-devel包，而update源https://dl.bintray.com/vmware/photon_updates_3.0_aarch64/不存在，最终由于安装mariadb组件失败导致编译退出。
   目前只能注释该Dakefile的这一部分，但是这将直接导致编译出来的goharbor/harbor-migrator镜像不可用，但这不影响docker-harbor的部署，因为这只是一个工具。

————————————————————

  This project exists because, currently, I can't find the images or offline packages for arm64 on the harbor release（https://github.com/goharbor/harbor/releases）. To meet my needs, I built the images and offline packages on  ARM64 device using https://github.com/goharbor/harbor source code,reference on https://github.com/goharbor/harbor/blob/master/docs/compile_guide.md .

Main Explanations:

1.Building needs to be done on ARM64 devices.

2.Building docker-compose for ARM64 reference on https://github.com/ubiquiti/docker-compose-aarch64.

3.CMD:make package_offline GOBUILDIMAGE=golang:1.9.2 COMPILETAG=compile_golangimage

4.version control 
'''
modify the parameter in Makefile:
VERSIONTAG : Harbor images tag, default: dev
PKGVERSIONTAG : Harbor online and offline version tag, default:dev
'''

5*Unresolved problems
  Building tools/migration Error, because The software source(https://dl.bintray.com/vmware/photon_release_3.0_aarch64/aarch64/) of photon:3.0-aarch64 tdnf doesn't have the packages of mariadb-server mariadb mariadb-devel,and the source of update:https://dl.bintray.com/vmware/photon_updates_3.0_aarch64/ doesn't seem to have been established.
  For skip building errors,I just commented and disabled the code of building image migration in Dockerfile on tools/migration.It will not affect the using of harbor, but it is not a good way to solving it.Hope you can make some suggestions.Thanks.
