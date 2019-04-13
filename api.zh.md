# WebTorrent 文档

WebTorrent是一个流媒体种子客户端，有**Node.js的**和**Web**两版本。WebTorrent在两种环境中，都提供相同的API。

要在浏览器中使用WebTorrent，需要支持[WebRTC]（Chrome，Firefox，Opera，Safari）。

[webrtc]: https://en.wikipedia.org/wiki/WebRTC

## Install

```bash
npm install webtorrent
```

## Quick Example

```js
var client = new WebTorrent()

var torrentId = 'magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent'

client.add(torrentId, function (torrent) {
  // Torrents can contain many files. Let's use the .mp4 file
  var file = torrent.files.find(function (file) {
    return file.name.endsWith('.mp4')
  })

  // Display the file by adding it to the DOM. Supports video, audio, image, etc. files
  file.appendTo('body')
})
```

# WebTorrent API

## `WebTorrent.WEBRTC_SUPPORT`

WebRTC是否在环境中本机支持？

```js
if (WebTorrent.WEBRTC_SUPPORT) {
  // WebRTC is supported
} else {
  // Use a fallback
}
```

## `client = new WebTorrent([opts])`

创建一个新的`WebTorrent`实例。

如果`opts`如果已指定，则将覆盖默认选项（如下所示）。

```js
{
  maxConns: Number,        // Max number of connections per torrent (default=55)
  nodeId: String|Buffer,   // DHT protocol node ID (default=randomly generated)
  peerId: String|Buffer,   // Wire protocol peer ID (default=randomly generated)
  tracker: Boolean|Object, // Enable trackers (default=true), or options object for Tracker
  dht: Boolean|Object,     // Enable DHT (default=true), or options object for DHT
  webSeeds: Boolean        // Enable BEP19 web seeds (default=true)
}
```

对于可能的值`opts.dht`看到了[`bittorrent-dht` documentation](https://github.com/webtorrent/bittorrent-dht#dht--new-dhtopts)。

对于可能的值`opts.tracker`看到了[`bittorrent-tracker` documentation](https://github.com/webtorrent/bittorrent-tracker#client)。

## `client.add(torrentId, [opts], [function ontorrent (torrent) {}])`

开始下载新的torrent。

`torrentId`可以是以下之一：

-   磁铁uri（弦）
-   种子文件（缓冲区）
-   info hash（十六进制字符串或缓冲区）
-   解析种子（来自[parse-torrent](https://github.com/webtorrent/parse-torrent)）
-   http / https url到torrent文件（String）
-   torrent文件到torrent文件的路径（String）*（仅限Node.js）*

如果`opts`如果已指定，则将覆盖默认选项（如下所示）。

```js
{
  announce: [String],        // Torrent trackers to use (added to list in .torrent or magnet uri)
  getAnnounceOpts: Function, // Custom callback to allow sending extra parameters to the tracker
  maxWebConns: Number,       // Max number of simultaneous connections per web seed [default=4]
  path: String,              // Folder to download files to (default=`/tmp/webtorrent/`)
  store: Function            // Custom chunk store (must follow [abstract-chunk-store](https://www.npmjs.com/package/abstract-chunk-store) API)
}
```

如果`ontorrent`指定，然后它将被调用**这个**torrent已准备好使用（即元数据可用）。注意：这与将要触发的'torrent'事件截然不同**所有**种子。

如果您希望立即访问torrent对象以便在从网络中获取元数据时侦听事件，则使用返回值`client.add`。如果您只想要文件数据，请使用`ontorrent`或'种子'事件。

如果你提供`opts.store`，它将被称为`opts.store(chunkLength, storeOpts)`有：

-   `storeOpts.length`-  torrent中所有文件的大小
-   `storeOpts.files`- 一组torrent文件对象
-   `storeOpts.torrent`- 存储的torrent实例

## `client.seed(input, [opts], [function onseed (torrent) {}])`

开始播种新的种子。

`input`可以是以下任何一种：

-   文件系统到文件或文件夹的路径（字符串）*（仅限Node.js）*
-   W3C[File](https://developer.mozilla.org/en-US/docs/Web/API/File)对象（来自`<input>`或拖放）*（仅限浏览器）*
-   W3C[FileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList)对象（基本上是一个数组`File`对象）*（仅限浏览器）*
-   节点[Buffer](https://nodejs.org/api/buffer.html)宾语
-   节点[Readable stream](https://nodejs.org/api/stream.html#stream_class_stream_readable)宾语

或者，一个**数组`string`，`File`，`Buffer`， 要么`stream.Readable`对象**。

如果`opts`如果指定，它应包含以下类型的选项：

-   选项[create-torrent](https://github.com/webtorrent/create-torrent#createtorrentinput-opts-function-callback-err-torrent-)（允许配置创建的.torrent文件）
-   选项`client.add`（往上看）

如果`onseed`如果已指定，则在客户端开始播种文件时将调用它。

**注意：**每个torrent都需要有一个名字。如果没有明确提供`opts.name`，将使用以下逻辑自动确定：

-   如果所有文件共享公共路径前缀，则将使用该前缀。例如，如果所有文件路径都以`/imgs/`种子名称将是`imgs`。
-   否则，具有名称的第一个文件将确定torrent名称。例如，如果第一个文件是`/foo/bar/baz.txt`，种子名称将是`baz.txt`。
-   如果没有文件有名称（比如所有文件都是Buffer或Stream对象），那么就像“Unnamed Torrent”这样的名字<id>“将会产生。

**注意：**每个文件都需要有一个名称。对于文件系统路径或W3C File对象，该名称包含在对象中。对于缓冲区或可读流类型，a`name`可以在对象上设置属性，如下所示：

```js
var buf = new Buffer('Some file content')
buf.name = 'Some file name'
client.seed(buf, cb)
```

## `client.on('torrent', function (torrent) {})`

当准备好使用torrent时发出（即元数据可用并且存储已准备好）。有关方法的更多信息，请参阅torrent部分`torrent`具有。

## `client.on('error', function (err) {})`

客户端遇到致命错误时发出。当发生这种情况时，客户端会自动销毁并清除所有种子并进行清理。

始终倾听'错误'事件。

## `client.remove(torrentId, [function callback (err) {}])`

从客户端删除torrent。销毁与对等体的所有连接并删除所有已保存的文件数据。如果`callback`如果已指定，则在删除文件数据时将调用它。

\*注意：此方法目前不会删除torrent数据（例如，`/tmp/webtorrent/...`，见`path`选项`client.add`）。在修复之前，请自行实施（考虑使用`rimraf`npm包）。

## `client.destroy([function callback (err) {}])`

摧毁客户端，包括所有种子和与同伴的连接。如果`callback`如果已指定，则在客户端正常关闭时将调用它。

## `client.torrents[...]`

一系列客户端的种子。

## `client.get(torrentId)`

返回给定的torrent`torrentId`。方便的方法。比搜索更容易`client.torrents`阵列。返回`null`如果找不到匹配的torrent。

## `client.downloadSpeed`

所有种子的总下载速度，以字节/秒为单位。

## `client.uploadSpeed`

所有种子的总上传速度，以字节/秒为单位。

## `client.progress`

所有人的总下载进度**活性**种子，从0到1。

## `client.ratio`

汇总所有种子的“种子比率”（上传/下载）。

# Torrent API

## `torrent.infoHash`

torrent的信息哈希（字符串）。

## `torrent.magnetURI`

torrent的磁力链（字符串）。

## `torrent.torrentFile`

`.torrent`种子的文件（缓冲区）。

## `torrent.torrentFileBlobURL` *(browser only)*

`.torrent`torrent文件（Blob URL）。

## `torrent.files[...]`

torrent中所有文件的数组。请参阅文档`File`下面了解哪些方法/属性文件。

## `torrent.timeRemaining`

下载完成的剩余时间（以毫秒为单位）。

## `torrent.received`

从对等端接收的总字节数（*包含*无效数据）。

## `torrent.downloaded`

总*验证*从对等端接收的字节。

## `torrent.uploaded`

上传到对等体的总字节数。

## `torrent.downloadSpeed`

Torrent下载速度，以字节/秒为单位。

## `torrent.uploadSpeed`

Torrent上传速度，以字节/秒为单位。

## `torrent.progress`

Torrent下载进度，从0到1。

## `torrent.ratio`

Torrent“种子比例”（上传/下载）。

## `torrent.numPeers`

torrent群中的对等体数量。

## `torrent.path`

Torrent下载位置。

## `torrent.destroy([callback])`

别名`client.remove(torrent)`。如果`callback`如果提供了，它将在种子被完全销毁时被调用，即所有打开的套接字都被关闭，并且存储被关闭。

## `torrent.addPeer(peer)`

将一个对等体添加到torrent群。这是高级功能。通常，您不需要打电话`torrent.addPeer()`手动。WebTorrent将使用跟踪服务器或DHT自动查找对等方。这仅用于手动将对等方添加到客户端。

直到该方法才应该调用此方法`infoHash`事件已经发出。

返回`true`如果添加了peer，`false`如果对等方被加载的阻止列表阻止。

该`peer`参数必须是格式中的地址字符串`12.34.56.78:4444`（对于普通的TCP / uTP对等体），或者a[`simple-peer`](https://github.com/feross/simple-peer)实例（对于WebRTC对等体）。

## `torrent.addWebSeed(url)`

将一个Web种子添加到torrent群。有关BitTorrent Web种子的更多信息，请参阅[BEP19](http://www.bittorrent.org/beps/bep_0019.html)。

在浏览器中，Web种子服务器必须具有适当的CORS（跨源资源共享）标头，以便可以跨域获取数据。

该`url`参数是Web种子URL。

## `torrent.removePeer(peer)`

从torrent群中删除对等体。这是高级功能。通常，您不需要打电话`torrent.removePeer()`手动。当它们很慢或者没有需要的部分时，WebTorrent会自动从种子群中删除对等体。

该`peer`参数应该是一个地址（即“ip：port”字符串），一个peer id（十六进制字符串）或者`simple-peer`实例。

## `torrent.select(start, end, [priority], [notify])`

选择一系列片段以优先开始`start`并以。结尾`end`在给定的情况下（包括两者）`priority`。`notify`是使用新数据更新选择时要调用的可选回调。

## `torrent.deselect(start, end, priority)`

Deprioritize一系列以前选择的作品。

## `torrent.critical(start, end)`

将一系列部分标记为要尽快下载的关键优先级。从`start`至`end`（包括在内）。

## `torrent.createServer([opts])`

创建一个http服务器来提供此torrent的内容，动态获取所需的torrent片段以满足http请求。支持范围请求。

返回一个`http.Server`实例（来自通话`http.createServer`）。如果`opts`如果指定，它可以具有以下属性：

```js
{
  origin: String // Allow requests from specific origin. `false` for same-origin. [default: '*']
  hostname: String // If specified, only allow requests whose `Host` header matches this hostname. Note that you should not specify the port since this is automatically determined by the server. Ex: `localhost` [default: `undefined`]
}
```

访问服务器的根目录`/`将显示指向单个文件的链接列表。访问单个文件`/<index>`哪里`<index>`是指数`torrent.files`数组（例如`/0`，`/1`等）

这是一个用法示例：

```js
var client = new WebTorrent()
var magnetURI = 'magnet: ...'

client.add(magnetURI, function (torrent) {
  // create HTTP server for this torrent
  var server = torrent.createServer()
  server.listen(port) // start the server listening to a port

  // visit http://localhost:<port>/ to see a list of files

  // access individual files at http://localhost:<port>/<index> where index is the index
  // in the torrent.files array

  // later, cleanup...
  server.close()
  client.destroy()
})
```

## `torrent.pause()`

暂时停止与新同行的连接。请注意，这不会暂停新的传入连接，也不会暂停现有连接或其连线的流。

## `torrent.resume()`

继续连接到新同行。

## `torrent.on('infoHash', function () {})`

已确定torrent的信息哈希时发出。

## `torrent.on('metadata', function () {})`

已确定torrent的元数据时发出。这包括.torrent文件的完整内容，包括文件列表，torrent长度，片段哈希，片段长度等。

## `torrent.on('ready', function () {})`

当种子准备好被使用时发出（即元数据可用并且存储准备就绪）。

## `torrent.on('warning', function (err) {})`

有警告时发出。这纯粹是信息性的，没有必要听这个事件，但它可能有助于调试。

## `torrent.on('error', function (err) {})`

当种子遇到致命错误时发出。当发生这种情况时，torrent会自动销毁并从客户端中删除。

**注意：**发出Torrent错误`torrent.on('error')`。如果torrent实例上没有“错误”事件处理程序，则会发出错误`client.on('error')`。这可以防止抛出未捕获的异常（未处理的'错误'事件），但这使得无法区分客户端错误与torrent错误。Torrent错误不是致命的，客户端之后仍然可以使用。因此，始终在两个地方听错（`client.on('error')`和`torrent.on('error')`）。

## `torrent.on('done', function () {})`

已下载所有torrent文件时发出。

这是一个用法示例：

```js
torrent.on('done', function(){
  console.log('torrent finished downloading')
  torrent.files.forEach(function(file){
     // do something with file
  })
})
```

## `torrent.on('download', function (bytes) {})`

下载数据时发出。用于报告当前的torrent状态，例如：

```js
torrent.on('download', function (bytes) {
  console.log('just downloaded: ' + bytes)
  console.log('total downloaded: ' + torrent.downloaded)
  console.log('download speed: ' + torrent.downloadSpeed)
  console.log('progress: ' + torrent.progress)
})
```

## `torrent.on('upload', function (bytes) {})`

每次上传数据时都会发出。用于报告当前的torrent状态。

## `torrent.on('wire', function (wire) {})`

每当为此torrent连接新对等端时发出。`wire`是一个实例[`bittorrent-protocol`](https://github.com/webtorrent/bittorrent-protocol)，这是到远程对等体的node.js样式双工流。此事件可用于指定[custom BitTorrent protocol extensions](https://github.com/webtorrent/bittorrent-protocol#extension-api)。

这是一个用法示例：

```js
var MyExtension = require('./my-extension')

torrent1.on('wire', function (wire, addr) {
  console.log('connected to peer with address ' + addr)
  wire.use(MyExtension)
})
```

见`bittorrent-protocol`
[extension api docs](https://github.com/webtorrent/bittorrent-protocol#extension-api)有关如何定义协议扩展的更多信息。

## `torrent.on('noPeers', function (announceType) {})`

每当DHT或跟踪器发布时都会发出，但没有找到同伴。`announceType`或者是`'tracker'`要么`'dht'`取决于触发此事件发生的通知。请注意，如果您尝试从跟踪器和DHT中发现对等体，您将分别为每个事件看到此事件。

# File API

## `file.name`

文件名，由torrent指定。*示例：'some-filename.txt'*

## `file.path`

文件路径，由torrent指定。*示例：'some-folder / some-filename.txt'*

## `file.length`

文件长度（以字节为单位），由torrent指定。*示例：12345*

## `file.downloaded`

总*验证*从该对象接收的字节，用于此文件。

## `file.progress`

文件下载进度，从0到1。

## `file.select()`

选择要下载的文件，但优先级低于带有流的文件。如果您知道稍后需要该文件，则非常有用。

## `file.deselect()`

取消选择该文件，这意味着除非有人为其创建流，否则不会下载该文件。

\*注意：此方法目前无法正常工作，请参阅[dcposch answer on #164](https://github.com/webtorrent/webtorrent/issues/164)为解决问题做了很好的工作。

## `stream = file.createReadStream([opts])`

创建一个[readable stream](https://nodejs.org/api/stream.html#stream_class_stream_readable)到文件。流所需的片段将被高度优先化并首先从群中获取。

你可以通过`opts`仅流式传输文件的一部分。

```js
{
  start: startByte,
  end: endByte
}
```

都`start`和`end`包容性。

## `file.getBuffer(function callback (err, buffer) {})`

获取文件内容为`Buffer`。

该文件将从具有最高优先级的网络中获取，并且`callback`文件准备好后将被调用。`callback`必须指定，并将使用a调用`Error`（要么`null`）和文件内容为`Buffer`。

```js
file.getBuffer(function (err, buffer) {
  if (err) throw err
  console.log(buffer) // <Buffer 00 98 00 01 ...>
})
```

## `file.appendTo(rootElem, [opts], [function callback (err, elem) {}])` *(browser only)*

通过将文件附加到DOM来在浏览器中显示该文件。这是一个功能强大的函数，可以处理许多文件类型，如视频（.mp4，.webm，.m4v等），音频（.m4a，.mp3，.wav等），图像（.jpg，.gif ,.

png等）和其他文件格式（.pdf，.md，.txt等）。该文件将从具有最高优先级的网络中获取并流入页面（如果是视频或音频）。在某些情况下，视频或音频文件将无法流式传输，因为它们不是浏览器可以流式传输的格式，因此文件将在播放前完全下载。

`rootElem`对于其他非流式文件类型（如图像和PDF），将下载文件然后显示。是一个容器元素（CSS选择器或对DOM节点的引用），将显示内容。将为内容创建一个新的DOM节点并附加到`rootElem`。

如果提供，`opts`可以包含以下选项：

-   `autoplay`：自动播放视频/音频文件（默认值：`false`）
-   `muted`：静音视频/音频文件（默认值：`false`）
-   `controls`：显示视频/音频播放器控件（默认值：`true`）
-   `maxBlobLength`：超过此大小的文件将跳过“blob”策略并失败（默认值：`200 * 1000 * 1000`字节）

注意：现代浏览器倾向于阻止带有音频自动播放的媒体（这里是[Chrome policy](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes)例如）所以如果你设置`autoplay`至`true`，这也是一个好主意`muted`至`true`。

如果提供，`callback`将在文件对用户可见时调用。`callback`被称为`Error`（要么`null`）以及显示内容的新DOM节点。

```js
file.appendTo('#containerElement', function (err, elem) {
  if (err) throw err // file failed to download or display in the DOM
  console.log('New DOM node with the content', elem)
})
```

流支持取决于支持`MediaSource`浏览器中的API。所有现代浏览器都有`MediaSource`支持。

对于视频和音频，webtorrent尝试了多种播放文件的方法：

-   [`videostream`][videostream]- 最佳选择，支持流媒体**寻求**，但现在仅适用于基于MP4的文件（使用`MediaSource`API）
-   [`mediasource`][mediasource]- 支持更多格式，支持流媒体**没有寻求**（用途`MediaSource`API）
-   Blob URL  - 支持所有格式（大多数格式）`<video>`标签支持来自http url），**寻求**但是**不支持流式传输**（必须先下载整个文件）

[videostream]: https://www.npmjs.com/package/videostream

[mediasource]: https://www.npmjs.com/package/mediasource

如果文件结束，则不会尝试Blob URL策略`opts.maxBlobLength`（默认为200 MB）因为它需要在播放开始之前下载整个文件，这样才能显示出来`<video>`标签被搁置。如果增加大小，请务必以某种方式在UI中向用户指示加载进度。

对于其他媒体格式，如图像，该文件只是添加到DOM。

对于基于文本的格式，如html文件，pdfs等，该文件通过沙盒添加到DOM`<iframe>`标签。

## `file.renderTo(elem, [opts], [function callback (err, elem) {}])` *(browser only)*

喜欢`file.appendTo`但直接渲染到给定元素（或CSS选择器）。例如，要呈现视频，请提供`<video>`元素喜欢`file.renderTo('video#player')`。

## `file.getBlob(function callback (err, blob) {})` *(browser only)*

获得W3C`Blob`包含文件数据的对象。

该文件将从具有最高优先级的网络中获取，并且`callback`文件准备好后将被调用。`callback`必须指定，并将使用a调用`Error`（要么`null`）和`Blob`宾语。

## `file.getBlobURL(function callback (err, url) {})` *(browser only)*

获取可在浏览器中使用的URL以引用该文件。

该文件将从具有最高优先级的网络中获取，并且`callback`文件准备好后将被调用。`callback`必须指定，并将使用a调用`Error`（要么`null`）和Blob URL（`String`）。

此方法对于创建文件下载链接很有用，如下所示：

```js
file.getBlobURL(function (err, url) {
  if (err) throw err
  var a = document.createElement('a')
  a.download = file.name
  a.href = url
  a.textContent = 'Download ' + file.name
  document.body.appendChild(a)
})
```
