# ZeroTier for KSU

用了各位大佬的模块，但是吧，老用命令行，不是很方便。正好赶上想学学vue，所有就做了这个给自己用。

感谢以下连接提供的帮助，顺序不分先后

- [是否有可能 Zerotier-One 直接在 Android 设备上运行？ - V2EX](https://v2ex.com/t/863131)
- [Android以太网和WIFI完美共存](https://blog.csdn.net/G_Rookie/article/details/109679262)
- [Network Management in Android: Routing](https://yotam.net/posts/network-management-in-android-routing/)
- [vant-ui/vant-demo](https://github.com/vant-ui/vant-demo/tree/master/vant/vite)
- [zfdx123/build-k40-ksu](https://github.com/zfdx123/build-k40-ksu)
- [eventlOwOp/zerotier-magisk](https://github.com/eventlOwOp/zerotier-magisk/tree/master/zerotier)
- [linuxscreen/ZeroTierOneForMagisk](https://github.com/linuxscreen/ZeroTierOneForMagisk)
- [taamarin/box_for_magisk](https://github.com/taamarin/box_for_magisk/blob/master/box/scripts/box.inotify)
- [stunnel/static-curl](https://github.com/stunnel/static-curl)

# 免责声明

本项目不对以下情况负责：设备变砖、SD 卡损坏或 SoC 烧毁。

# 使用方法

用UI界面

# 一些可选操作说明

## 文件说明

### Zerotier数据目录:`/data/adb/zerotier`；虽然UI都实现了，但是还是说明下，给自己备忘下；在该目录下创建以下文件可以做到

    创建文件`/data/adb/zerotier/KEEP_ON_UNINSTALL`，卸载模块可保留数据目录
    创建文件`/data/adb/zerotier/MANMANUAL`，关闭开机自启
    创建文件`/data/adb/zerotier/ALLOW_9993`，iptables放行UDP 9993入端口

## 执行脚本说明

### 执行所有脚本都需要带全路径

    `sh /data/adb/modules/ZeroTierForKSU/zerotier.sh`

```shell

 # 通过webapi接口调用zerotier服务
sh /data/adb/modules/ZeroTierForKSU/api.sh $1 other(可选参数如下)
  status)
    status
    return 自定义的状态接口，放回给页面用的参数
    ;;
  networks)
    return 查询网络详情，如果传入具体的网络id，则返回单个详情，不传就返回所有已加入的节点详情
    networks $2
    ;;
  leaveNetwork)
    离开网络，传具体的网络ID
    leaveNetwork $2
    ;;
  joinOrUpdateNetwork)
    加入网络或者更新网络，第一个参数是网络ID，第二个参数json对象，{    "allowDNS": false,    "allowDefault": false,    "allowManaged": true,   "allowGlobal": false,    "name": '',    "id": ''  }
    joinOrUpdateNetwork $2 ''$3''
    ;;
  peer)
    返回成员列表
    peer
    ;;
  firewall)
    防火墙规则,能传 A(增加) 和 D(删除)
    firewall $2 
    ;;
  router)
    zerotier路由模式 ，能传两个参数， 第一个参数 0 （没实现）新建zerotier ip rule 表，1提升main表优先级，第二个参数 add 新增，del 删除
    router $@
    ;;
  orbit)
    加入自建的moon，需要一个参数，自建moon的网络id
    orbit $@
    ;;
```

    `sh /data/adb/modules/ZeroTierForKSU/zerotier-cli` #同官方
    `sh /data/adb/modules/ZeroTierForKSU/zerotier-idtool` #同官方
    `sh /data/adb/modules/ZeroTierForKSU/zerotier.inotify` # 没弄，本来想弄快速开关的
