# Shadowsocks客户端通用逻辑

下面就来对使用ss技术时所涉及到的客户端的各种通用逻辑来详细解释一下：

## ss客户端使用ss服务的配置信息包含哪些

有了ss客户端，想要用ss服务的话，前提是你已经有了对应的ss服务器的配置信息

最最基本的ss服务器的配置信息至少包括：

* 服务器的地址：一般是IP或域名
* 服务器的端口号
* 加密方式：常见都有`aes-256-cfb`、`chacha20-ietf-poly1305`等等
* 密码

然后把这些配置信息，添加到ss的客户端中，就可以使用ss了。

## 加密方式：`aes-256-cfb` 和 `chacha20-ietf-poly1305`

在介绍如何用ss客户端之前，先对于**加密方式**做个详细的解释，否则会导致下载了客户端，但不支持新的加密方式，而无法使用的问题。

ss技术本身不限制你采用何种加密方式去加密数据。

目前主流的ss服务器端所采用的加密方式，其实更多的还是：`aes-256-cfb`

而有些ss服务，现在是采用最新的加密方式：`chacha20-ietf-poly1305`

对比来说就是：

* 之前旧的加密方式是：`aes-256-cfb`
  * 最常见，使用的最为广泛
    * 所以一般的ss的客户端也都支持
      * 比如之前我就用过的：
        * Mac的ShadowsocksX
        * Android的`影梭`
  * 但是不是足够复杂和安全
* 现在新的加密方式是：`chacha20-ietf-poly1305`
  * 相对来说，更加复杂，但也更安全
  * 但是：
    * 很多旧版本客户端都不支持
      * 换句话说：
        * 如果你的ss服务用的是`chacha20-ietf-poly1305`加密方式，但你用的客户端不支持`chacha20-ietf-poly1305`（即使支持`chacha20-ietf`也不行），那就没法使用ss了
    * 只有一些新版的客户端才支持，包括：
      * `Mac`：[macOS shadowsocksX-NG 1.6.1+](https://github.com/shadowsocks/ShadowsocksX-NG/releases)
      * `Windows`：[Shadowsocks-Windows 4.0.6+](https://github.com/shadowsocks/shadowsocks-windows/releases)
      * `Android`：[Shadowsocks Android 4.2.5+](https://github.com/shadowsocks/shadowsocks-android/releases)
      * `iOS`：最新版`shadowrocket` 或`Potatso`/`Potatso Lite`

## 添加ss服务配置信息的方式

对于ss客户端中去添加上述ss服务器的配置信息，有多种方式：

### 添加订阅+更新订阅 实现一次性添加所有服务器节点

后来知道了一个更加先进和方便的添加服务器节点的办法：

* 添加订阅地址
  * 前提：需要购买的服务器支持订阅
    * 会有一个普通网址一样的订阅地址
  * 然后即可去客户端端添加订阅地址
* 更新订阅
  * 即可瞬间，批量添加所有的服务器节点

### 手动（一个一个）添加（ss服务器配置信息）

对于上述的ss服务器的配置信息，可以一个个手动的去输入。

典型的方式是，一个个复制和粘贴对应的ss服务器的地址，端口号，选择对应的加密方式，粘贴密码等等，去手动添加配置信息。

### 扫（描二维）码（添加单个ss服务器配置信息）

一般的购买到的ss的第三方服务，都提供了二维码，某个二维码是对应ss服务器的配置信息根据一定规则生成的

-> 所以ss客户端如果支持扫码添加的话，即可去扫码，内部自动解析配置，从而自动添加该ss服务器配置信息

和上面的手动的复制和粘贴相比，肯定是通过扫码去添加配置，要方便多了。

### 批量导入（导入单个json配置文件实现一次性添加多个服务器配置信息）

ss客户端支持的话，可以去利用别人（比如我自己去添加多个服务器配置后，去导出）弄好的配置信息（一般是json文件），然后直接导入配置文件，即可实现批量添加多个ss服务器配置信息了。并且，同时也把其他ss客户端的其他设置信息也添加进来了，更是方便。

和上面的手动或扫码比，批量的导入，当然是更加方便了。