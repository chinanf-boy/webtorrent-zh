# 常提问题

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


  - [WebTorrent 是什么?](#webtorrent-%E6%98%AF%E4%BB%80%E4%B9%88)
  - [有啥，这很酷吗?](#%E6%9C%89%E5%95%A5%E8%BF%99%E5%BE%88%E9%85%B7%E5%90%97)
  - [WebTorrent 有哪些使用示例吗?](#webtorrent-%E6%9C%89%E5%93%AA%E4%BA%9B%E4%BD%BF%E7%94%A8%E7%A4%BA%E4%BE%8B%E5%90%97)
  - [现今，谁使用 WebTorrent?](#%E7%8E%B0%E4%BB%8A%E8%B0%81%E4%BD%BF%E7%94%A8-webtorrent)
  - [WebTorrent 是怎么工作的?](#webtorrent-%E6%98%AF%E6%80%8E%E4%B9%88%E5%B7%A5%E4%BD%9C%E7%9A%84)
  - [那我要怎么开始了?](#%E9%82%A3%E6%88%91%E8%A6%81%E6%80%8E%E4%B9%88%E5%BC%80%E5%A7%8B%E4%BA%86)
  - [WebRTC 是什么?](#webrtc-%E6%98%AF%E4%BB%80%E4%B9%88)
  - [WebTorrent 客户端能与正常 BitTorrent 客户端连接吗?](#webtorrent-%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%83%BD%E4%B8%8E%E6%AD%A3%E5%B8%B8-bittorrent-%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%BF%9E%E6%8E%A5%E5%90%97)
  - [不同网站的 WebTorrent 客户端能连接到彼此吗?](#%E4%B8%8D%E5%90%8C%E7%BD%91%E7%AB%99%E7%9A%84-webtorrent-%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%83%BD%E8%BF%9E%E6%8E%A5%E5%88%B0%E5%BD%BC%E6%AD%A4%E5%90%97)
  - [谁构建 WebTorrent?](#%E8%B0%81%E6%9E%84%E5%BB%BA-webtorrent)
  - [WebTorrent, LLC 是什么?](#webtorrent-llc-%E6%98%AF%E4%BB%80%E4%B9%88)
  - [WebTorrent 又与 PeerCDN 有什么不同?](#webtorrent-%E5%8F%88%E4%B8%8E-peercdn-%E6%9C%89%E4%BB%80%E4%B9%88%E4%B8%8D%E5%90%8C)
  - [我怎样帮个忙?](#%E6%88%91%E6%80%8E%E6%A0%B7%E5%B8%AE%E4%B8%AA%E5%BF%99)
  - [哪里我能学到更多?](#%E5%93%AA%E9%87%8C%E6%88%91%E8%83%BD%E5%AD%A6%E5%88%B0%E6%9B%B4%E5%A4%9A)
  - [WebTorrent 支持序列流. 影响网络?](#webtorrent-%E6%94%AF%E6%8C%81%E5%BA%8F%E5%88%97%E6%B5%81-%E5%BD%B1%E5%93%8D%E7%BD%91%E7%BB%9C)
  - [为什么WebTorrent，没有被设计成一个全新的现代协议呢？?](#%E4%B8%BA%E4%BB%80%E4%B9%88webtorrent%E6%B2%A1%E6%9C%89%E8%A2%AB%E8%AE%BE%E8%AE%A1%E6%88%90%E4%B8%80%E4%B8%AA%E5%85%A8%E6%96%B0%E7%9A%84%E7%8E%B0%E4%BB%A3%E5%8D%8F%E8%AE%AE%E5%91%A2)
  - [可以用 WebTorrent 进行实时流媒体吗?](#%E5%8F%AF%E4%BB%A5%E7%94%A8-webtorrent-%E8%BF%9B%E8%A1%8C%E5%AE%9E%E6%97%B6%E6%B5%81%E5%AA%92%E4%BD%93%E5%90%97)
  - [使用VPN时，WebTorrent 是否泄漏您的IP地址？我听说 WebRTC 泄露了你的IP地址。](#%E4%BD%BF%E7%94%A8vpn%E6%97%B6webtorrent-%E6%98%AF%E5%90%A6%E6%B3%84%E6%BC%8F%E6%82%A8%E7%9A%84ip%E5%9C%B0%E5%9D%80%E6%88%91%E5%90%AC%E8%AF%B4-webrtc-%E6%B3%84%E9%9C%B2%E4%BA%86%E4%BD%A0%E7%9A%84ip%E5%9C%B0%E5%9D%80)
- [遇到麻烦了](#%E9%81%87%E5%88%B0%E9%BA%BB%E7%83%A6%E4%BA%86)
  - [为什么浏览器下载，不起作用？我看不到对端!](#%E4%B8%BA%E4%BB%80%E4%B9%88%E6%B5%8F%E8%A7%88%E5%99%A8%E4%B8%8B%E8%BD%BD%E4%B8%8D%E8%B5%B7%E4%BD%9C%E7%94%A8%E6%88%91%E7%9C%8B%E4%B8%8D%E5%88%B0%E5%AF%B9%E7%AB%AF)
  - [为什么视频/音频流不工作?](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A7%86%E9%A2%91%E9%9F%B3%E9%A2%91%E6%B5%81%E4%B8%8D%E5%B7%A5%E4%BD%9C)
  - [问题不断?](#%E9%97%AE%E9%A2%98%E4%B8%8D%E6%96%AD)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## WebTorrent 是什么?

**WebTorrent**是第一个在**浏览器**中，运行的种子客户端。 是的，没错。浏览器。

它完全用 javascript 编写，并使用**WebRTC**，做到真正的点对点传输。不需要浏览器插件、扩展或安装包。

使用开放的 Web 标准，WebTorrent 将网站用户连接在一起，形成一个分布式的、分散的浏览器到浏览器网络，以实现高效的文件传输。

## 有啥，这很酷吗?

想象一下，像 YouTube 这样的视频网站，**若访问者能帮助，持有网站内容**。 紧接着，支持 WebTorrent 网站的用户越多，网站的速度越快，抗性越强。

浏览器到浏览器的通信，**排除中间人**，让人们用自己的方式交流。没有更多的客户端/服务器 —— 只是一个对等网络。WebTorrent 是通往[再分散性][redecentralize]网络的第一步。

> 我们对网络的编码方式将，决定我们的网络生活的方式。所以，我们需要将我们的价值烘焙到代码中。将表达自由，变成需要，融入我们的代码中。隐私应该融入我们的代码中。自由获取所有知识。但是如今，这些理想，并没有嵌入到 Web 。
>
> <cite>-Brewster Kahle，互联网档案的创始人（来自[锁住了 Web 的开放性][brewster]）

## WebTorrent 有哪些使用示例吗?

WebTorrent 最令人兴奋的用途之一是**对端-辅助传输**。 非盈利项目[维基百科][wikipedia]以及[互联网档案][archive]，可以通过让访问者加入，来降低带宽和托管成本。流行的内容，可通过浏览器到浏览器，提供服务，速度快且成本低。少量的访问内容，通过 HTTP，由源服务器可靠地提供服务。

还有令人兴奋的**商业用例**，从 CDN 到 应用程序发送。

> WebTorrent 具有巨大的商务潜力，可以通过内部基础设施和外部封闭用户通信的应用程序，彻底改变客户端-服务器的传统概念。WebTorrent 已经从一个“想法”变成了一个科学实验，现在正处于可行的边缘。这真的很酷。
>
> <cite>-Chris Kranky（来自[“WebTorrent:重新思考传输”][kranky-article]）</cite>

[wikipedia]: https://www.wikipedia.org/
[archive]: https://archive.org/index.php
[kranky-article]: https://www.chriskranky.com/webtorrent-rethinking-delivery/
[redecentralize]: http://redecentralize.org/about/
[brewster]: https://blog.archive.org/2015/02/11/locking-the-web-open-a-call-for-a-distributed-web/

## 现今，谁使用 WebTorrent?

WebTorrent 仍然是相当新的，但它已经被用在了，很酷的方式上：

| 名                                              | 曰                                                                                                 |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **[WebTorrent Desktop][webtorrent-desktop]**    | 流媒体 Torrent 应用程序。给 Mac、Windows 和 Linux。（[源代码][webtorrent-desktop-source]）         |
| **[Instant.io][instant.io]**                    | 通过 WebTorrent，传输流文件（[源代码][instant.io-source]）                                         |
| **[GitTorrent][gittorrent]**                    | 使用 BitTorrent 和 Bitcoin 的 分散式 Github（[源代码][gittorrent-source]）                         |
| **[PeerCloud][peercloud]**                      | 利用 WebTorrent 的无服务器网站（[源代码][peercloud-source]）                                       |
| **[File.pizza][filepizza]**                     | 在浏览器中，免费进行点对点文件传输（[源代码][filepizza-source]）                                     |
| **[Webtorrentapp][webtorrentapp]**              | 从 Torrents 启动 Web 应用程序的平台                                                            |
| **[Fastcast][fastcast]**                        | 带一些视频，的画廊网站（[源代码][fastcast-source]）                                                  |
| **[Colored Coins][coloredcoins]**               | 在区块链上，创建数字资产的开放协议（[源代码][coloredcoins-source]）                                  |
| **[Tokenly Pockets][pockets]**                  | 基于 WebTorrent 元数据的数字令牌发布（[源代码][pockets-source]）                                   |
| **[βTorrent][btorrent]**                        | 功能齐全的 WebTorrent 浏览器客户端（[源代码][btorrent-source]）                                    |
| **[Zapsnap][zapsnap]**                          | 浏览器，共享临时点对点屏幕截图（[源代码][zapsnap-source]）                                         |
| **[PeerWeb][peerweb]**                          | 从 Torrent 获取，并呈现静态网站                                                                      |
| **[Niagara][niagara]**                          | 带字幕的视频播放器 （zipped.srt（s））。                                                 |
| **[Vique][vique]**                              | 视频播放器队列，以共享视频                                                                           |
| **[YouShark][youshark]**                        | 用于 WebTorrent 的 Web 音乐播放器（[源代码][youshark-source]）                                     |
| **[Peerify][peerify]**                          | 为你的文件，即时网络播种                                                                              |
| **[Instant-Share][instant-share]**              | 通过 WebTorrent ，共享文件                                                                           |
| **[P2PDrop][p2pdrop]**                          | 在对端之间，安全共享文件（[源代码][p2pdrop-source]）                                               |
| **[Twister][twister]**                          | 分散式微博服务，使用 WebTorrent 作为媒体附件（[源代码][twister-source]）                           |
| **[PeerTube][peertube]**                        | Web 浏览器中，分散式视频流平台的原型（[源代码][peertube-source]）                                    |
| **[Cinematrix][cinematrix]**                    | 流式播放，您最喜爱的免费内容                                                                         |
| **[webtorrent-cljs][webtorrent-cljs]**          | WebTorrent 的 ClojureScript 包                                                                   |
| **[Squidlink][squidlink]**                      | 不使用云，将文件从 A 传输到 B（[源代码][squidlink-source]）                                          |
| **[Web2web][web2web]**                          | 无服务器和无域网站，可通过 Torrents 和比特币区块链更新（[源代码][web2web-source]）                   |
| **[Magnet Player][magnet-player]**              | 直接从浏览器，传输视频流（[源代码][magnet-player-source]）                                           |
| **[PeerFast][peerfast]**                        | 第一次 P2P 网速测试（[源代码][peerfast-source]）                                                   |
| **[TorrentMedia][torrentmedia]**                | 功能齐全的 WebTorrent 桌面客户端                                                                   |
| **[Gaia 3D Star Map][gaia]**                    | 200 万颗星，使用 WebGL、WebVR 和 WebTorrent 进行 3D 渲染                                           |
| **[Watchtor][watchtor]**                        | 网上种子观看的极简方法（[源代码][watchtor-source]）                                                |
| **[CacheP2P][cachep2p]**                        | 高度分布式，缓存平台（[源代码][cachep2p-source]）                                                    |
| **[DropClickPaste][dropclickpaste]**            | 拖放简单内容共享                                                                                   |
| **[LocalFiles][localfiles]**                    | 通过将文件，固定到地理位置，来共享文件                                                                 |
| **[WebTorrent Google Cast (WTGC)][wtgc]**       | 在谷歌广播设备上，播放 WebTorrent 媒体（[源代码][wtgc-source]）                                      |
| **[WebTorrent Player][webtorrent-player]**      | 由 Angular2 和 Ngrx 构建的 WebTorrent 播放器（[源代码][webtorrent-player-source]）                 |
| **[CodeDump][codedump]**                        | 基于 WebTorrent 的，代码粘贴程序（[源代码][codedump-source]）                                        |
| **[Lunik-Torrent][lunik-torrent]**              | WebTorrent 下载程序和文件管理器。（[源代码][lunik-torrent-source]）                                |
| **[BitChute][bitchute]**                        | 分散的视频流社交网络                                                                               |
| **[Planktos][planktos]**                        | 允许网站通过， BitTorrent 提供静态内容（[源代码][planktos-source]）                                  |
| **[SuperQuickShare][superquickshare]**          | 使用 WebTorrent 和 QRCodes 在设备之间，快速共享文件（[源代码][superquickshare-source]）              |
| **[P2P-CDN][p2pcdn]**                           | webtorrent 优雅降级的cdn                                                                  |
| **[PearPlayer][pearplayer]**                    | 基于多源 WebTorrent 的多协议 P2P 流媒体播放器                                                      |
| **[Tcloud][tcloud]**                            | 文件共享，和 种子下载                                                                            |
| **[Webtorrent-webui][webtorrent-webui]**        | 具有简单 Web 界面的 WebTorrent 客户端，远程使用                                                |
| **[CineTimes][cinetimes]**                      | 公共域电影，流媒体网站                                                                             |
| **[Bitlove.org][bitlove]**                      | 您最喜欢的 BitTorrent 播客                                                                         |
| **[lofiTorrent][lofitorrent]**                  | 在线和离线 Torrent 浏览器客户端                                                                    |
| **[Live-torrent][live-torrent]**                | WebTorrent 支持的直播流解决方案的简单实现（[源代码][live-torrent-source]）                         |
| **[CDNBye][cdnbye]**                            | 使用类似于 BitTorrent 的协议，通过点对点网络，实现 WebRTC 数据通道，来扩展实时/VOD 视频流。 |
| **[Files.fm][files.fm]**                        | 快速文件共享，和免费增值云存储服务，使用 P2P 技术，加速无限下载和文件分发。                            |
| **[imgest][imgest]**                            | 使用 JavaScript 和 WebTorrent 构建的无服务器共享图像库。                                           |
| **[Bugout][bugout]**                            | 在浏览器选项卡中，生成和运行后端 Web 服务。                                                          |
| **[P2P Media Loader][p2p-media-loader]**        | 用于 hls.js 和 shaka 播放器的引擎，支持通过 hls 或 dash 协议，共享实时和 VOD 流的 P2P。              |
| **[Cheff][cheff]**                              | 在设备之间，共享食物配方。[source code](https://github.com/vasco3/cheff)                             |
| ***您的应用程序-用你的网址！[发送请求][pr]*吧** |

#### WebTorrent 生产替代方案

这里还列出了 WebTorrent 支持的集中式服务替代方案：[WebTorrent 复刻产品][webtorrent-clones]

[webtorrent-clones]: https://github.com/DiegoRBaquero/awesome-webtorrent-clones
[webtorrent-desktop]: https://webtorrent.io/desktop
[webtorrent-desktop-source]: https://github.com/webtorrent/webtorrent-desktop
[instant.io-source]: https://github.com/webtorrent/instant.io
[gittorrent]: http://blog.printf.net/articles/2015/05/29/announcing-gittorrent-a-decentralized-github/
[gittorrent-source]: https://github.com/cjb/GitTorrent
[filepizza]: http://file.pizza/
[filepizza-source]: https://github.com/kern/filepizza
[peercloud]: https://peercloud.io/
[peercloud-source]: https://github.com/jhiesey/peercloud
[webtorrentapp]: https://github.com/alexeisavca/webtorrentapp
[fastcast]: http://fastcast.nz
[fastcast-source]: https://github.com/fastcast/fastcast
[coloredcoins]: http://coloredcoins.org
[coloredcoins-source]: https://github.com/Colored-Coins/Metadata-Handler
[pockets]: https://tokenly.com/
[pockets-source]: https://github.com/loon3/Tokenly-Pockets
[btorrent]: https://btorrent.xyz
[btorrent-source]: https://github.com/DiegoRBaquero/bTorrent
[zapsnap]: http://zapsnap.io/
[zapsnap-source]: https://github.com/twobucks/zapsnap
[peerweb]: https://github.com/retrohacker/peerweb.js
[niagara]: https://andreapaiola.name/niagara/
[vique]: https://andreapaiola.name/vique/
[youshark]: http://youshark.neocities.org/
[youshark-source]: https://github.com/enorrmann/youshark
[peerify]: https://peerify.btorrent.xyz
[instant-share]: http://fs.lunik.xyz/
[p2pdrop]: http://p2pdrop.com
[p2pdrop-source]: https://github.com/ajainvivek/P2PDrop
[twister]: http://twister.net.co/?p=589
[twister-source]: https://github.com/miguelfreitas/twister-html
[peertube]: http://peertube.cpy.re
[peertube-source]: https://github.com/Chocobozzz/PeerTube
[cinematrix]: http://cinematrix.one/
[webtorrent-cljs]: https://github.com/cvillecsteele/webtorrent-cljs
[squidlink]: http://squidl.ink
[squidlink-source]: https://github.com/darkenvy/Squidl.ink
[web2web]: https://elendirx.github.io/web2web
[web2web-source]: https://github.com/elendirx/web2web
[magnet-player]: https://ferrolho.github.io/magnet-player/
[magnet-player-source]: https://github.com/ferrolho/magnet-player/
[peerfast]: https://diegorbaquero.github.io/PeerFast/#
[peerfast-source]: https://github.com/DiegoRBaquero/PeerFast
[torrentmedia]: https://github.com/FaCuZ/torrentmedia
[gaia]: http://charliehoey.com/threejs-demos/gaia_dr1.html
[watchtor]: https://open-watchtor.hashbase.io
[watchtor-source]: https://github.com/codealchemist/watchtor
[cachep2p]: http://www.cachep2p.com/
[cachep2p-source]: https://github.com/guerrerocarlos/CacheP2P
[dropclickpaste]: http://dropclickpaste.com/
[localfiles]: https://localfiles.alhur.es/
[wtgc]: https://wtgc.firebaseapp.com
[wtgc-source]: https://git.io/wtgc
[webtorrent-player]: http://webtorrent-player.s3-website-us-east-1.amazonaws.com/
[webtorrent-player-source]: https://github.com/Hongbo-Miao/webtorrent-player
[codedump]: http://ronsoros.github.io
[codedump-source]: https://github.com/ronsoros/ronsoros.github.io/blob/master/index.html
[lunik-torrent]: https://tcloud-lunik.herokuapp.com
[lunik-torrent-source]: https://github.com/Lunik/Lunik-Torrent
[bitchute]: https://www.bitchute.com
[planktos]: https://xuset.github.io/planktos/
[planktos-source]: https://github.com/xuset/planktos
[superquickshare]: https://sqs.fun
[superquickshare-source]: https://github.com/manicphase/super-quick-share
[p2pcdn]: https://github.com/andreapaiola/P2P-CDN
[pearplayer]: https://github.com/PearInc/PearPlayer.js
[tcloud]: https://github.com/Lunik/tcloud
[webtorrent-webui]: https://github.com/pldubouilh/webtorrent-webui
[cinetimes]: http://cinetimes.org/
[bitlove]: https://bitlove.org/
[lofitorrent]: https://lofitorrent.js.org/
[live-torrent]: https://live.computer
[live-torrent-source]: https://github.com/pldubouilh/live-torrent
[cdnbye]: https://github.com/cdnbye/hlsjs-p2p-engine
[files.fm]: https://files.fm
[imgest]: https://imgest.hashbase.io
[bugout]: https://github.com/chr15m/bugout
[p2p-media-loader]: https://github.com/novage/p2p-media-loader
[cheff]: https://cheff.cuadranteweb.com

## WebTorrent 是怎么工作的?

WebTorrent 协议的工作原理与[BitTorrent 协议][bittorrent-protocol]相仿，除了它使用[WebRTC][webrtc]而不是[（TCP）传输控制协议][tcp]/[uTP][utp]作为传输协议。

为了支持[WebRTC 的 连接模型][webrtc-signaling]，我们对跟踪协议做了一些修改。因此，基于浏览器的 WebTorrent 客户端或 **“Web 对端/对等端”**只能连接到支持 WebTorrent/WebRTC 的其他客户端。

我们所更改的协议，将作为[BEP](http://www.bittorrent.org/beps/bep_0001.html)发布。 在编写规范之前，可以查看[`bittorrent-tracker`][bittorrent-tracker]包。

一旦连接了对等端，用于通信的有线协议，与正常 BitTorrent 中的协议完全相同。这应该会让，现有流行的 Torrent 客户端（如 Transmission）和 Autocurrent ，更容易添加对 WebTorrent 的支持。**Vuze**
[已经支持了][vuze-support] WebTorrent！

![WebTorrent network diagram](https://webtorrent.io/img/network.png)

[bittorrent-protocol]: https://wiki.theory.org/BitTorrentSpecification
[webrtc-signaling]: http://www.html5rocks.com/en/tutorials/webrtc/infrastructure/#what-is-signaling
[tcp]: https://en.wikipedia.org/wiki/Transmission_Control_Protocol
[utp]: https://en.wikipedia.org/wiki/Micro_Transport_Protocol
[webrtc]: https://en.wikipedia.org/wiki/WebRTC
[bittorrent-tracker]: https://npmjs.com/package/bittorrent-tracker
[vuze-support]: https://wiki.vuze.com/w/WebTorrent

## 那我要怎么开始了?

要开始使用 WebTorrent，只需在网页包含 [`webtorrent.min.js`](https://cdn.jsdelivr.net/webtorrent/latest/webtorrent.min.js)脚本。如果你使用[browserify](http://browserify.org/)你可以`npm install webtorrent`和`require('webtorrent')`.

下载种子 ，并将其添加到页面，会很容易。

```js
var client = new WebTorrent();

var torrentId =
  'magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent';

client.add(torrentId, function(torrent) {
  // Torrents can contain many files. Let's use the .mp4 file
  var file = torrent.files.find(function(file) {
    return file.name.endsWith('.mp4');
  });
  file.appendTo('body'); // append the file to the DOM
});
```

它支持视频、音频、图像、PDF、Markdown，还有[更多][render-media]正要从口袋拿出来。有其他直接访问文件内容的方法，包括作为 node-样式的流媒体、Buffer 或 Blob url。

可以传输流式视频和音频内容，即在下载完整文件之前，开始播放。播种也能工作 —— 能给予 WebTorrent 动态地，从网络按需获取所需的种子片段。

## WebRTC 是什么?

WebRTC（Web 实时通信(Real-Time Communication)）是由万维网联盟（W3C）定义的一个 API，用于支持浏览器到浏览器的应用程序，如语音呼叫、视频聊天和 P2P 文件共享，而无需浏览器插件。

WebRTC 的`RTCDataChannel`API 允许直接将数据从一个浏览器传输到另一个浏览器。这和`WebSocket`和`XMLHttpRequest`不同，因为它们是为与服务器（即客户端-服务器模型）通信而设计的。而数据通道(RTCDataChannel)允许**直接浏览器到浏览器的连接**.

这是一场革命。以前，网站从未能以超低延迟、加密，点对点地直接将用户连接到彼此。这将在医疗、教育、科学等领域，实现下一代应用。WebTorrent 只是一个例子。

WebRTC[能在任何地方工作][webrtc-everywhere]，和浏览器支持非常好。**Chrome**，**火狐**和**Opera** ，不管是 PC 还是 Android，以及**微软 Edge**和**Safari**都会有支持。

您可以在以下网址，了解有关 WebRTC 数据通道的更多信息：[HTML5 Rocks][datachannel-intro].

[webrtc-everywhere]: https://speakerdeck.com/feross/webrtc-everywhere-beyond-the-browser-at-data-terra-nemo-2015
[datachannel-intro]: http://www.html5rocks.com/en/tutorials/webrtc/datachannels/

## WebTorrent 客户端能与正常 BitTorrent 客户端连接吗?

在浏览器中，WebTorrent 只能，下载由 WebRTC 支持的 Torrent 客户端的种子。

现在，我们知道这些支持 WebRTC 的 Torrent 客户端：

| 名                                                        | 曰                                                              |
| --------------------------------------------------------- | --------------------------------------------------------------- |
| **[WebTorrent Desktop][webtorrent-desktop]**              | 开源的流式 Torrent 客户端。给 Mac、Windows 和 Linux。           |
| **[Vuze][vuze-support]**                                  | 功能强大、功能齐全的 Torrent 客户端                             |
| **[Playback][playback]**                                  | 开源 javascript 视频播放器**（超级酷！）**                      |
| **[`webtorrent-hybrid`][webtorrent-hybrid]**              | node.js 包（命令行和 api）                                      |
| **[Instant.io][instant.io]**                              | 网站中的简单 WebTorrent 客户端                                  |
| **[βTorrent][btorrent]**                                  | 功能齐全的浏览器 WebTorrent 客户端（[源代码][btorrent-source]） |
| **[TorrentMedia][torrentmedia]**                          | 桌面 WebTorrent 客户端                                          |
| _即将推出更多产品-[发送公关][pr]将您的客户添加到列表中！_ |

### 关于 `webtorrent-hybrid` 的 小只是

在 node.js 中，`webtorrent-hybrid`可以从 WebRTC 对等端或 TCP 对等端（即普通对等端）下载种子。您可以将 WebTorrent 用作命令行程序，或用作 node.js 包编程。

安装`webtorrent-hybrid`在终端中，运行以下命令（添加`-g`安装命令行程序的标志，省略该标志，会以本地安装）：

```
npm install webtorrent-hybrid -g
```

注意：如果您只需要在浏览器中使用 webtorrent（webrtc 原生可用的），则用[`webtorrent`][webtorrent]替代，它的安装速度更快，因为它，不需要安装 WebRTC (node)实现。

## 不同网站的 WebTorrent 客户端能连接到彼此吗?

当然可以！**WebTorrent 在整个 Web 上工作。**在一个域上运行的 WebTorrent 客户端，可以连接到任何其他域上的客户端。没有哭泣！

同源策略，不适用于 WebRTC 连接，因为它们不是客户端到服务器的连接。浏览器到浏览器的连接，需要两个网站的合作（即，WebTorrent 脚本，必须同时出现在两个网站上）。

## 谁构建 WebTorrent?

WebTorrent 是由[Feross Aboukhadijeh][feross]以及数百个开源贡献者共同构建的。WebTorrent 项目由[WebTorrent，LLC][webtorrent-io]管理，作为一个非盈利项目。

Feross 的其他项目包括[javascript 标准样式][standard]，[PeRCDN][peercdn]（卖给雅虎）[学习笔记][studynotes]和[YouTube 即时通讯][ytinstant].

在过去，Feross 参与[斯坦福大学][stanford]，在[斯坦福人机交互][hci]和[计算机安全][seclab]实验室做过研究，并在[Quora][quora]，[脸谱网][facebook]和[英特尔][intel]工作。

[standard]: http://standardjs.com/
[studynotes]: https://www.apstudynotes.org/
[ytinstant]: http://ytinstant.com/
[stanford]: http://www.stanford.edu/
[hci]: http://hci.stanford.edu/
[seclab]: http://seclab.stanford.edu/
[quora]: https://www.quora.com/
[facebook]: https://www.facebook.com/
[intel]: http://intel.com/

##  WebTorrent, LLC 是什么?

“WebTorrent，LLC”是拥有 WebTorrent 的合法实体。WebTorrent 是，而且永远是，**非营利、开源和免费软件**.

目前，还没有从 WebTorrent 中获利的计划。

## WebTorrent 又与 PeerCDN 有什么不同?

[PeRCDN][peercdn]是由 WebRTC 支持的下一代 cdn，用于高效地，点对点传输网站内容。Peercdn 由[Feross Aboukhadijeh][feross]，[Abi Raja][abi]和[John Hiesey][jhiesey] 2013 年 3 月创建，并于2013 年 12 月出售给[雅虎][yahoo]。

WebTorrent 是由[Feross Aboukhadijeh][feross]2013 年 10 月。不像 PeerCDN，**WebTorrent 是免费软件**，根据[MIT 许可][license]. 你可以随心所欲地使用它！

> “免费软件”是自由的问题，而不是价格。要理解这个概念，你应该把“自由”看成是“言论自由”，而不是“免费啤酒”。
>
> <cite>-Richard Stallman，软件自由行动者</cite>

在技术层面上，peercdn 和 webtorrent 的构建，考虑了不同的目标。peercdn 针对低延迟下载，和快速对端发现，进行了优化。这意味着客户端和站点所有者，信任集中式服务器，可以将文件 URL 映射到内容哈希。

另一方面，WebTorrent 不需要客户端信任集中式服务器。只要给定一个`.torrent`文件或磁力链接，WebTorrent 客户端下载文件时，不信任任何服务器或对端。

[feross]: http://feross.org/
[abi]: http://abiraja.com/
[jhiesey]: https://github.com/jhiesey
[yahoo]: https://www.yahoo.com/

## 我怎样帮个忙?

WebTorrent 是一个**开源项目**. 做出重要和有价值贡献的个人，将被授予承诺访问项目的权限，以便在他们认为合适的时候做出贡献。（详见全文）[贡献者指南][contributing]）

有很多方法，可以帮助你！

- 报告错误[创建 GitHub 问题][issues].
- 编写代码，[解决未解决的问题][open-issues].

如果您正在寻求帮助，请加入我们[gitter][gitter]或，在 IRC 上`#webtorrent`（freenode）以及如何开始。

[open-issues]: https://github.com/webtorrent/webtorrent/issues?state=open
[contributing]: https://github.com/webtorrent/webtorrent/blob/master/CONTRIBUTING.md

## 哪里我能学到更多?

网上有很多关于 WebTorrent 的讲座。这里有几个：

### 介绍 BitTorrent 和 WebTorrent (JSConf)

<iframe width="853" height="480" src="https://www.youtube.com/embed/kxHRATfvnlw?rel=0" frameborder="0" allowfullscreen></iframe>

### WebRTC 到处都是: 凌驾浏览器 (slides only)

<script async class="speakerdeck-embed" data-id="cb08869f2ac2445c99e8b73a4ac65d2b" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

## WebTorrent 支持序列流. 影响网络?

BitTorrent 客户端使用一种称为“最稀有优先”的算法，来选择要下载的文件片段。系统中的每一个对等端，都会先尝试下载最稀有的部分，平均下来，在网络中大多数部分的可用性大致相同。

在实践中，稀有优先算法对 不良的种子，最为重要，或者在发布种子的前几个小时（当，播种/获种的比率不好时）。

大多数 Torrent 客户端都支持一些特性，而这些特性导致它偏离了稀有优先算法。例如，可以选择/取消选择，或排序/降级， Torrent 中的某些文件。

WebTorrent 支持按顺序传输 Torrent 文件，这对播放媒体文件来说很有用。我们正致力于改进算法，在没有对特定部分的高优先级需求时，切换回稀有优先的策略。换言之，当缓冲了足够的介质时，我们可以使用普通的“稀有优先”选择的算法。

但事实是，随着当今互联网连接的速度，用户只需花费很少的时间就可以完全下载 Torrent。，因此他们仍将花费比下载更多的时间播种。

另请注意：BitTorrent 公司的官方 Torrent 客户端 utorrent ，是提供顺序下载和选择性文件下载，BitTorrent 网络仍然非常健康。

## 为什么WebTorrent，没有被设计成一个全新的现代协议呢？?

BitTorrent 是目前最成功、部署最广泛的 P2P 协议。它真的很管用。我们 WebTorrent 的目标是以与现有 Torrent 网络互操作的方式，将 BitTorrent 引入 Web。

重新发明该协议，会让 WebTorrent 从根本上与现有客户端不兼容，且方案不予通过。我们现在这样做更好。有线协议是完全相同的，只不过除了现有的 TCP 和 UTP 之外，现在有了一种新的连接到对等端的方法：WebRTC。

此外，重新发明协议是一个巨大的兔子坑。当我们开始这个项目的时候，已经有了很大的风险 —— WebRTC 会被所有的浏览器供应商所采用吗？数据通道实现。是否稳定，并得以执行？javascript 是否足够快，可以动态重新打包 MP4 视频，以便使用 MediaSource API 进行流式播放？我们的想法是：为什么要在标准中，添加一个新的有线协议和一些算法？

的确，BitTorrent 协议在某些方面是过时的。例如，它使用自己的奇怪的数据编码，称为“bencoding”。如果它是今天发明的，它可能，会h使用 JSON 或 messagepack。但是，这并不重要——BitTorrent 工作得很好，我们更关心的是，构建健壮有用的软件，而不是概念上的纯粹性，或追求最新的软件时尚。

## 可以用 WebTorrent 进行实时流媒体吗?

WebTorrent 不能进行，开箱即用的实时流，但是您可以在 WebTorrent 之上，构建实时流解决方案。

种子是不变的。这意味着一旦创建了一个 Torrent 文件，就不能，在不更改信息哈希的情况下更改它。那么，怎样，才能绕过这个限制呢？

一个天真的方法是：内容生产者，可以每 10 秒获取一次实时内容，并为其创建一个种子。浏览者将遵循Torrent 文件的这个“feed” （或信息散列）并按顺序下载内容。流媒体播放，将在实时流之后约 10-20 秒。

不过，这种方法，肯定可以改进！为什么不自己试一试，分享代码呢？

## 使用VPN时，WebTorrent 是否泄漏您的IP地址？我听说 WebRTC 泄露了你的IP地址。

不。

WebRTC 数据通道，不允许网站在使用 VPN 时，发现您的公共 IP 地址。WebRTC 发现过程，只会找到您的 VPN 的 IP 地址和本地网络 IP 地址。

本地 IP 地址（例如 10.x.x.x 或 192.168.x.x）可能用于“指纹化”浏览器，并在您访问的不同站点之间，进行识别，如第三方跟踪 cookie。但是，这是一个与公开，真实公共 IP 地址不同的问题，值得注意的是，浏览器已经为您提供了，数百个指纹化识别的向量（例如，您安装的字体、屏幕分辨率、浏览器窗口大小、操作系统版本、语言等）。

如果您启用了 VPN，那么 WebRTC 数据通道，将不会使用您真正的公共 IP 地址，连接到对等端，也不会显示在网页上，运行的 javascript 中。

有一次，webrtc 确实遇到了一个问题，它允许一个网站，发现你真正的公共 IP 地址，但这个问题在很久以前，就已经解决了。但这种不幸的错误信息在互联网上，不断反弹。

现在有了一个规范，它精确定义了 WebRTC 公开的 IP 地址。如果你对进一步阅读感兴趣，你可以阅读[IP 控制规范](https://tools.ietf.org/html/draft-ietf-rtcweb-ip-handling-01)。

# 遇到麻烦了

## 为什么浏览器下载，不起作用？我看不到对端!

它确实有效！但你不能只使用任何随机磁力 uri 或`.torrent`文件。Torrent 必须，由支持 WebRTC 的客户端（即[WebTorrent 桌面][webtorrent-desktop]，[Vuze][vuze-support]，[WebTorrent 混合][webtorrent-hybrid]，[Playback][playback]，[即时通讯][instant.io]或[β 种子][btorrent]) 播种。

在浏览器中，webtorrent 只能通过支持 webrtc 的客户端，下载明确播种到 web 对端的种子。 种子桌面客户端，需要支持 WebRTC 才能连接到 Web 浏览器。

## 为什么视频/音频流不工作?

流媒体的支持，取决浏览器中的 `MediaSource` API。所有现代浏览器都有`MediaSource`支持。在 firefox 中，firefox 42 增加了支持（即 firefox nightly）。

也支持[许多文件类型][render-media]（同样，取决于浏览器支持），但仅支持`.mp4`，`.m4v`和`.m4a`全力支持，包括播种。

为了支持任意文件的视频/音频流，WebTorrent 使用[`videostream`][videostream]包，该包又使用了[`mp4box.js`][mp4box.js]。 如果您认为其中一个包中，可能存在错误，请在相应的存储库中，提交一个问题。

[videostream]: https://npmjs.com/package/videostream
[mp4box.js]: https://github.com/gpac/mp4box.js

## 问题不断?

在 WebTorrent [问题跟踪器][issues]打开一个问题，或者加入我们[gitter][gitter],或在 IRC 上`#webtorrent`（freenode）

[webtorrent-io]: https://webtorrent.io
[render-media]: https://github.com/feross/render-media/blob/master/index.js
[gitter]: https://gitter.im/webtorrent/webtorrent
[instant.io]: https://instant.io
[issues]: https://github.com/webtorrent/webtorrent/issues
[license]: https://github.com/webtorrent/webtorrent/blob/master/LICENSE
[peercdn]: http://www.peercdn.com/
[playback]: https://mafintosh.github.io/playback/
[pr]: https://github.com/webtorrent/webtorrent
[webtorrent-hybrid]: https://npmjs.com/package/webtorrent-hybrid
[webtorrent]: https://npmjs.com/package/webtorrent
