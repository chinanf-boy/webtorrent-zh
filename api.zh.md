# WebTorrent 文档

WebTorrent 是一个流式种子客户端，有**Node.js 的**和**Web**两版本。WebTorrent 在两种环境中，都提供相同的 API。

要在浏览器中使用 WebTorrent，需要支持[WebRTC]（Chrome，Firefox，Opera，Safari）。

[webrtc]: https://en.wikipedia.org/wiki/WebRTC

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [WebTorrent API](#webtorrent-api)
- [Torrent API](#torrent-api)
- [File API](#file-api)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 安装

```bash
npm install webtorrent
```

## 快示例

```js
var client = new WebTorrent();

var torrentId =
  'magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent';

client.add(torrentId, function(torrent) {
  // Torrents can contain many files. Let's use the .mp4 file
  var file = torrent.files.find(function(file) {
    return file.name.endsWith('.mp4');
  });

  // Display the file by adding it to the DOM. Supports video, audio, image, etc. files
  file.appendTo('body');
});
```

# WebTorrent API

## `WebTorrent.WEBRTC_SUPPORT`

WebRTC 是否在环境中，原生支持？

```js
if (WebTorrent.WEBRTC_SUPPORT) {
  // WebRTC 支持
} else {
  // Use a fallback
}
```

## `client = new WebTorrent([opts])`

创建一个新的`WebTorrent`实例。

如果`opts`已指定，则覆盖默认选项（如下所示）。

```js
{
  maxConns: Number,        // 每个种子连接的最大数 (默认=55)
  nodeId: String|Buffer,   // DHT 协议 node ID (默认=随机生成)
  peerId: String|Buffer,   // Wire 协议 peer ID (默认=随机生成)
  tracker: Boolean|Object, // 启动 trackers (默认=true), 或是给 Tracker 的配置对象
  dht: Boolean|Object,     // 启动 DHT (默认=true), 或是给DHT的配置对象
  webSeeds: Boolean        // 启动 BEP19 web 种子 (默认=true)
}
```

对`opts.dht`可能的值，请看[`bittorrent-dht` 文档](https://github.com/webtorrent/bittorrent-dht#dht--new-dhtopts)。

对`opts.tracker`可能的值，请看[`bittorrent-tracker` 文档](https://github.com/webtorrent/bittorrent-tracker#client)。

## `client.add(torrentId, [opts], [function ontorrent (torrent) {}])`

开始下载新的 torrent。

`torrentId`可以是以下之一：

- 磁力链接（字符串）
- 种子文件（buffer）
- 信息哈希（十六进制字符串或 buffer）
- 解析种子（来自[parse-torrent](https://github.com/webtorrent/parse-torrent)）
- http/https 网址：torrent 文件（字符串）
- 文件系统路径：torrent 文件（字符串）_（仅限 Node.js）_

如果`opts`已指定，则将覆盖默认选项（如下所示）。

```js
{
  announce: [String],        // 要用的 种子追踪器 (添加到 .torrent 或 磁力链接的 网址列表)
  getAnnounceOpts: Function, // 自定义回调函数，允许发送额外参数到追踪器
  maxWebConns: Number,       // 每个 web 种子 同时连接的最大数  [默认=4]
  path: String,              // 下载到的目录 (默认=`/tmp/webtorrent/`)
  store: Function            // 自定义分块存储 (必须遵守 [abstract-chunk-store](https://www.npmjs.com/package/abstract-chunk-store) API)
}
```

了`ontorrent`，然后当**这个**种子已准备好的时候，它将被调用（即元数据可用）。注意：这与**所有**种子触发的'torrent'事件，截然不同。

如果，您希望立即访问 torrent 对象，以便在从网络中获取元数据时，侦听事件，则使用`client.add`的返回值。如果您只想要文件数据，请使用`ontorrent`或'torrent'事件。

如果你提供`opts.store`，会以`opts.store(chunkLength, storeOpts)`调用：

- `storeOpts.length`- 种子中所有文件的大小
- `storeOpts.files`- 种子的一组文件对象
- `storeOpts.torrent`- 存储的 torrent 实例

## `client.seed(input, [opts], [function onseed (torrent) {}])`

开始播种，新的种子。

`input`可以是，以下任何一种：

- 文件系统路径，可以是文件或文件夹（字符串）_（仅限 Node.js）_
- W3C [File](https://developer.mozilla.org/en-US/docs/Web/API/File)对象（来自`<input>`或拖放）_（仅限浏览器）_
- W3C [FileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList)对象（基本上是，一个`File`对象数组）_（仅限浏览器）_
- Node [Buffer](https://nodejs.org/api/buffer.html)对象
- Node [Readable stream](https://nodejs.org/api/stream.html#stream_class_stream_readable)对象

或者，一个**`string`，`File`，`Buffer`，要么`stream.Readable`对象的数组**。

如果`opts，它应包含以下类型的选项：

- [create-torrent](https://github.com/webtorrent/create-torrent#createtorrentinput-opts-function-callback-err-torrent-)选项（允许配置，创建的 .torrent 文件）
- `client.add`选项（往上看）

如果`onseed`已指定，则在客户端开始播种文件时，将调用它。

**注意：**每个 torrent 都需要有一个名字。如果没有明确提供`opts.name`，将使用以下逻辑，自动确定：

- 如果所有文件，共享一个公共路径前缀，则将使用该前缀。例如，如果所有文件路径都以`/imgs/`，那种子名称将是`imgs`。
- 否则，具有名称的第一个文件，将确定 torrent 名称。例如，如果第一个文件是`/foo/bar/baz.txt`，种子名称将是`baz.txt`。
- 如果没有文件有名称（比如所有文件都是 Buffer 或 Stream 对象），那么就像"Unnamed Torrent"，这样的名字<id>"将会产生。

**注意：**每个文件，都需要有一个名称。对于文件系统路径或 W3C File 对象，该名称会包含在对象中。对于 buffer 或可读流(stream)类型，可以在对象上设置一个`name`属性，如下所示：

```js
var buf = new Buffer('Some file content');
buf.name = 'Some file name';
client.seed(buf, cb);
```

## `client.on('torrent', function (torrent) {})`

当准备好使用 torrent 时，触发（即元数据可用，并且存储已准备好）。有关方法的更多信息，请参阅"`torrent`有什么方法"中的 torrent 部分。

## `client.on('error', function (err) {})`

客户端遇到致命错误时，触发。当发生这种情况时，客户端会自动销毁，并清除并进行清理所有种子。

始终监听'error'事件。

## `client.remove(torrentId, [function callback (err) {}])`

从客户端删除 torrent。销毁与对端的所有连接，并删除所有已保存的文件数据。如果`callback`已指定，则在删除文件数据时，将调用它。

\*注意：此方法目前，不会删除 torrent 数据（例如，`/tmp/webtorrent/...`，见`client.add`的`path`选项）。在修复之前，请自行实施（考虑使用`rimraf` npm 包）。

## `client.destroy([function callback (err) {}])`

摧毁客户端，包括所有种子和，对端的连接。如果`callback`已指定，则在客户端正常关闭时，将调用它。

## `client.torrents[...]`

数组，客户端的种子。

## `client.get(torrentId)`

返回给定 torrent`torrentId`的种子。方便的方法。比搜索`client.torrents`数组更容易。如果找不到匹配的 torrent，返回`null`。

## `client.downloadSpeed`

所有种子的，总下载速度，以字节/秒为单位。

## `client.uploadSpeed`

所有种子的，总上传速度，以字节/秒为单位。

## `client.progress`

所有**活性**种子的，总下载进度，从 0 到 1 。

## `client.ratio`

汇总，所有 torrent 的"种子比率"（上传/下载）。

# Torrent API

## `torrent.infoHash`

torrent 的信息哈希（字符串）。

## `torrent.magnetURI`

torrent 的磁力链接（字符串）。

## `torrent.torrentFile`

torrent 的 `.torrent`文件（Buffer）。

## `torrent.torrentFileBlobURL` _(仅限浏览器)_

torrent 的 `.torrent`文件（（Blob URL）。

## `torrent.files[...]`

torrent 中的数组，有所有文件(file)。请参阅下面的[`File`文档](#File-API)，了解它有哪些方法/属性。

## `torrent.timeRemaining`

下载完成的剩余时间（以 ms 为单位）。

## `torrent.received`

从对等端接收的总字节数（*包含*无效数据）。

## `torrent.downloaded`

*验证*从对等端接收的总字节。

## `torrent.uploaded`

上传到，对端的总字节数。

## `torrent.downloadSpeed`

Torrent 的下载速度，以字节/秒为单位。

## `torrent.uploadSpeed`

Torrent 的上传速度，以字节/秒为单位。

## `torrent.progress`

Torrent 的下载进度，从 0 到 1。

## `torrent.ratio`

Torrent 的"比例"（上传/下载）。

## `torrent.numPeers`

torrent 群中的对端数量。

## `torrent.path`

Torrent 下载位置。

## `torrent.destroy([callback])`

`client.remove(torrent)`的别名。如果`callback`提供了，它将在种子被完全销毁时，被调用，即所有打开的套接字都被关闭，并且存储被关闭。

## `torrent.addPeer(peer)`

将一个对端，添加到 torrent 群。这是高级功能。通常，您不需要手动调用`torrent.addPeer()`。WebTorrent 将使用跟踪服务器，或 DHT 自动查找对端。这仅用于，手动将对端添加到客户端。

直到`infoHash`事件已经触发，才应该调用此方法。

如果添加了对端，返回`true`，和对端被阻止加载列表，阻止，就是`false`。

`peer`参数，必须是`12.34.56.78:4444`格式的地址字符串（普通的 TCP/uTP 对端），或者 一个[`simple-peer`](https://github.com/feross/simple-peer)实例（WebRTC 对端）。

## `torrent.addWebSeed(url)`

将一个 Web 种子添加到 torrent 群。有关 BitTorrent Web 种子的更多信息，请参阅[BEP19](http://www.bittorrent.org/beps/bep_0019.html)。

在浏览器中，Web 种子服务器，必须具有适当的 CORS（跨源资源共享）标头，以便可以跨域获取数据。

`url`参数，是 Web 种子 URL。

## `torrent.removePeer(peer)`

从 torrent 群中删除对端。这是高级功能。通常，您不需要手动调用`torrent.removePeer()`。当它们很慢或者没有需要的部分时，WebTorrent 会自动从种子群中，删除对端。

`peer`参数应该是一个地址（即"ip：port"字符串），一个 peer id（十六进制字符串）或者`simple-peer`实例。

## `torrent.select(start, end, [priority], [notify])`

在给定`priority`的情况下，选择一系列片段，优先`start`开始，并`end`结束（包括在内）。`notify`是使用新数据更新选择时，要调用的可选回调。

## `torrent.deselect(start, end, priority)`

取消，一系列以前选择的。

## `torrent.critical(start, end)`

将一系列部分标记为，要尽快下载的重优先级。从`start`到`end`（包括在内）。

## `torrent.createServer([opts])`

创建一个 http 服务器，来提供此 torrent 的内容，动态获取所需的 torrent 片段，以满足 http 请求。支持范围请求。

返回一个`http.Server`实例（来自`http.createServer`调用）。如果`opts`指定，它可以具有以下属性：

```js
{
  origin: String; // 允许，特定源的请求. `false` 表示同源. [默认: '*']
  hostname: String; // 若指定了, 只允许 `Host`标头匹配该字符串的. 注意不要指定端口，因服务器会自行决定. Ex: `localhost` [默认: `undefined`]
}
```

访问服务器的根目录`/`将显示，指向单个文件的链接列表。用`/<index>`访问单个文件，这里的`<index>`是`torrent.files`数组的索引（例如`/0`，`/1`等）

这是一个用法示例：

```js
var client = new WebTorrent();
var magnetURI = 'magnet: ...';

client.add(magnetURI, function(torrent) {
  // 为这些 种子，创建 HTTP server
  var server = torrent.createServer();
  server.listen(port); // 开始监听端口

  // 访问 http://localhost:<port>/ 查看文件列表

  // 通过 http://localhost:<port>/<index> 访问对应索引的文件

  // 然后，记得清理...
  server.close();
  client.destroy();
});
```

## `torrent.pause()`

暂时停止，与新对端的连接。请注意，这不会暂停新的传入连接，也不会暂停现有连接或其连线的流。

## `torrent.resume()`

继续连接，到新对端。

## `torrent.on('infoHash', function () {})`

已确定 torrent 的信息哈希时，触发。

## `torrent.on('metadata', function () {})`

已确定 torrent 的元数据时，触发。这包括 .torrent 文件的完整内容，包括文件列表，torrent 长度，片段哈希，片段长度等。

## `torrent.on('ready', function () {})`

当种子准备好被使用时，触发（即元数据可用并且存储准备就绪）。

## `torrent.on('warning', function (err) {})`

有警告时，触发。这纯粹是信息性的，没有必要听这个事件，但它可能有助于调试。

## `torrent.on('error', function (err) {})`

当种子遇到致命错误时，触发。当发生这种情况时，torrent 会自动销毁，并从客户端中删除。

**注意：** Torrent 错误，会触发`torrent.on('error')`。如果 torrent 实例上，没有"error"事件处理程序，则会触发`client.on('error')`的事件。这可以防止，抛出未捕获的异常（未处理的'错误'事件），但这会无法区分，客户端错误与 torrent 错误。Torrent 错误不是致命的，因客户端之后，仍然可以使用。因此，始终在（`client.on('error')`和`torrent.on('error')`）两个地方监听错误。

## `torrent.on('done', function () {})`

已下载所有 torrent 文件时，触发。

这是一个用法示例：

```js
torrent.on('done', function() {
  console.log('torrent finished downloading');
  torrent.files.forEach(function(file) {
    // do something with file
  });
});
```

## `torrent.on('download', function (bytes) {})`

下载数据时，触发。用于报告当前的 torrent 状态，例如：

```js
torrent.on('download', function(bytes) {
  console.log('just downloaded: ' + bytes);
  console.log('total downloaded: ' + torrent.downloaded);
  console.log('download speed: ' + torrent.downloadSpeed);
  console.log('progress: ' + torrent.progress);
});
```

## `torrent.on('upload', function (bytes) {})`

每次上传数据时，都会触发。用于报告当前的 torrent 状态。

## `torrent.on('wire', function (wire) {})`

每当该 torrent ，有新对等端连接时，触发。`wire`是一个[`bittorrent-protocol`](https://github.com/webtorrent/bittorrent-protocol)实例，这是到远程对端的 node.js 样式双工流。此事件可用于指定[自定义 BitTorrent 协议扩展](https://github.com/webtorrent/bittorrent-protocol#extension-api)。

这是一个用法示例：

```js
var MyExtension = require('./my-extension');

torrent1.on('wire', function(wire, addr) {
  console.log('connected to peer with address ' + addr);
  wire.use(MyExtension);
});
```

见`bittorrent-protocol`
[扩展 api 文档](https://github.com/webtorrent/bittorrent-protocol#extension-api)中，有关如何定义协议扩展的更多信息。

## `torrent.on('noPeers', function (announceType) {})`

每当 DHT 或跟踪器出现，但却没有找到对端时，都会触发。`announceType`会是`'tracker'`或`'dht'`值，取决于事件的出现者。请注意，如果您尝试，从跟踪器和 DHT 中发现对端，您要搞清谁 v 触发事件的。

# File API

> 以下，指代的"文件"一词，有时是指'file' - 这个数值与内容集一身的 file 对象 。

## `file.name`

文件名，由 torrent 指定。_示例：'some-filename.txt'_

## `file.path`

文件路径，由 torrent 指定。_示例：'some-folder/some-filename.txt'_

## `file.length`

文件长度（以字节为单位），由 torrent 指定。_示例：12345_

## `file.downloaded`

*验证*从对端接收此文件的总字节。

## `file.progress`

文件下载进度，从 0 到 1。

## `file.select()`

选择要下载的文件，但优先级会低于流式文件。如果您知道稍后要该用文件，则非常有用。

## `file.deselect()`

取消选择该文件，这意味着，除非有人为其创建一个 stream ，否则不会下载该文件。

\*注意：此方法目前无法正常工作，请参阅[dcposch 在 #164 的回答](https://github.com/webtorrent/webtorrent/issues/164)，曲线救国。

## `stream = file.createReadStream([opts])`

为文件，创建一个[可读 stream](https://nodejs.org/api/stream.html#stream_class_stream_readable)。stream 所需的片段会是高优先化，并首先从种子群中获取。

你可以传递`opts`到 stream，限制仅传输文件的一部分。

```js
{
  start: startByte,
  end: endByte
}
```

`start`和`end`也会被包括。

## `file.getBuffer(function callback (err, buffer) {})`

把文件内容，整成一个`Buffer`。

该文件具有网络获取的最高优先级，并且文件准备好后，`callback`将被调用。`callback`必须指定，并会以一个`Error`（要么`null`）和一个`Buffer`文件内容参数，所调用。

```js
file.getBuffer(function(err, buffer) {
  if (err) throw err;
  console.log(buffer); // <Buffer 00 98 00 01 ...>
});
```

## `file.appendTo(rootElem, [opts], [function callback (err, elem) {}])` _(仅限浏览器)_

通过将文件附加到 DOM ，在浏览器中显示该文件。这是一个功能强大的函数，可以处理许多文件类型，如视频（.mp4，.webm，.m4v 等），音频（.m4a，.mp3，.wav 等），图像（.jpg，.gif , .png 等）和其他文件格式（.pdf，.md，.txt 等）。

该文件具有网络获取的最高优先级，和会 流(steram)入页面（如果是视频或音频的话）。在某些情况下，视频或音频文件，无法流式传输，因为它们不是浏览器，可以流式传输的格式，因此文件会在播放前，完全下载。对于其他非流式文件类型（如图像和 PDF），将下载文件然后显示。

`rootElem`是一个容器元素（CSS 选择器，或对 DOM Node 的引用），用于显示(文件)内容。会为内容创建一个新的 DOM Node ，并附加到`rootElem`。

若要提供`opts`的话，可以包含以下选项：

| 名              | 曰                                                                            |
| --------------- | ----------------------------------------------------------------------------- |
| `autoplay`      | 自动播放视频/音频文件（默认值：`false`）                                      |
| `muted`         | 静音视频/音频文件（默认值：`false`）                                          |
| `controls`      | 显示视频/音频播放器控件（默认值：`true`）                                     |
| `maxBlobLength` | 超过此大小的文件，将跳过"blob"策略，并失败（默认值：`200 * 1000 * 1000`字节） |

注意：现代浏览器倾向于阻止，带有音频自动播放的媒体（这里是[Chrome 策略](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes)示例）所以如果你设置`autoplay`到`true`，把`muted`到`true`，也是一个好主意。

若提供`callback`的话，它会在文件对用户可见时，调用。`callback`以一个`Error`（要么`null`）和一个显示内容的新 DOM Node 参数，所调用。

```js
file.appendTo('#containerElement', function(err, elem) {
  if (err) throw err; // 下载或展示 DOM 失败
  console.log('New DOM node with the content', elem);
});
```

流媒体的支持，取决于浏览器中的`MediaSource` API 支持。所有现代浏览器都有`MediaSource`支持。

对于视频和音频，webtorrent 尝试了多种播放文件的方法：

- [`videostream`][videostream]- 最佳选择，支持**播种**流媒体，但现在，仅适用于基于 MP4 的文件（使用`MediaSource`API）
- [`mediasource`][mediasource]- 支持更多格式，支持**不能播种**流媒体（使用`MediaSource`API）
- Blob URL - 支持大多数格式 ( http url 的`<video>`标签所支持的任意格式），**能播种**，但是**不支持流式传输**（必须先下载整个文件）

[videostream]: https://www.npmjs.com/package/videostream
[mediasource]: https://www.npmjs.com/package/mediasource

如果文件大于`opts.maxBlobLength`（默认为 200 MB），则不会尝试 Blob URL 策略，因为它需要在播放开始之前下载整个文件，这样才能显示出来。不然`<video>`标签被搁置。如果增加大小，请务必以某种方式在 UI 中，向用户指示加载进度。

对于其他媒体格式，如图像，file 只是添加到 DOM。

对于基于文本的格式，如 html 文件，pdfs 等，该文件通过沙盒`<iframe>`标签，添加到 DOM。

## `file.renderTo(elem, [opts], [function callback (err, elem) {}])` _(仅限浏览器)_

就像`file.appendTo`，但直接渲染到给定元素（或 CSS 选择器）。例如，要呈现视频，请提供`<video>`元素，像这样`file.renderTo('video#player')`。

## `file.getBlob(function callback (err, blob) {})` _(仅限浏览器)_

获得 包含文件数据的 W3C`Blob`对象。

该文件具有网络获取的最高优先级，并且文件准备好后，`callback`将被调用。`callback`必须指定，并会以一个`Error`（要么`null`）和一个`Blob`对象参数，所调用。

## `file.getBlobURL(function callback (err, url) {})` _(仅限浏览器)_

获取可在浏览器中使用的 URL ，该链接会引用文件。

该文件具有网络获取的最高优先级，并且文件准备好后，`callback`将被调用。`callback`必须指定，并会以一个`Error`（要么`null`）和 Blob URL（`String`）参数，所调用。

此方法对创建文件下载链接，很有用，如下所示：

```js
file.getBlobURL(function(err, url) {
  if (err) throw err;
  var a = document.createElement('a');
  a.download = file.name;
  a.href = url;
  a.textContent = 'Download ' + file.name;
  document.body.appendChild(a);
});
```
