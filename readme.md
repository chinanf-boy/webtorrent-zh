# webtorrent/webtorrent [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 来自 webtorrent/webtorrent (js) 的 播种技术，让我们开始在网上播种吧。」

[中文](./readme.zh.md) | [english](https://github.com/webtorrent/webtorrent)

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'webtorrent/webtorrent' -->
<!-- commit = 'e87a390a73000c84f14b8e419577a12d7d55720b' -->
<!-- time = '2018.11.13' -->

| 翻译的原文 | 与日期        | 最新更新 | 更多                       |
| ---------- | ------------- | -------- | -------------------------- |
| [commit]   | ⏰ 2018.11.13 | ![last]  | [中文翻译][translate-list] |

[last]: https://img.shields.io/github/last-commit/webtorrent/webtorrent.svg
[commit]: https://github.com/webtorrent/webtorrent/tree/e87a390a73000c84f14b8e419577a12d7d55720b

<!-- doc-templite END generated -->

> 文档来自 `webtorrent/webtorrent/blob/master/docs`

- [x] get-started.zh.md > readme.md
- [ ] [api 文档](api.zh.md)
- [x] [faq](faq.zh.md)
- [x] [种子库](free-torrents.zh.md)

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [开始使用 WebTorrent](#%E5%BC%80%E5%A7%8B%E4%BD%BF%E7%94%A8-webtorrent)
  - [安装](#%E5%AE%89%E8%A3%85)
    - [Browserify](#browserify)
  - [快例子](#%E5%BF%AB%E4%BE%8B%E5%AD%90)
    - [下载一个 torrent (在浏览器)](#%E4%B8%8B%E8%BD%BD%E4%B8%80%E4%B8%AA-torrent-%E5%9C%A8%E6%B5%8F%E8%A7%88%E5%99%A8)
    - [创建一个 torrent(种子) 和 播种 (在浏览器)](#%E5%88%9B%E5%BB%BA%E4%B8%80%E4%B8%AA-torrent%E7%A7%8D%E5%AD%90-%E5%92%8C-%E6%92%AD%E7%A7%8D-%E5%9C%A8%E6%B5%8F%E8%A7%88%E5%99%A8)
    - [下载和保存 一个 torrent (Node.js)](#%E4%B8%8B%E8%BD%BD%E5%92%8C%E4%BF%9D%E5%AD%98-%E4%B8%80%E4%B8%AA-torrent-nodejs)
    - [完整的网页示例](#%E5%AE%8C%E6%95%B4%E7%9A%84%E7%BD%91%E9%A1%B5%E7%A4%BA%E4%BE%8B)
    - [HTML 示例：状态显示 UI](#html-%E7%A4%BA%E4%BE%8B%E7%8A%B6%E6%80%81%E6%98%BE%E7%A4%BA-ui)
  - [更多文档](#%E6%9B%B4%E5%A4%9A%E6%96%87%E6%A1%A3)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 开始使用 WebTorrent

**WebTorrent**是第一个在**浏览器**工作的 torrent 客户端。它很容易上手！

## 安装

要开始使用 WebTorrent，只需在你的页面中，包含[`webtorrent.min.js`](https://cdn.jsdelivr.net/webtorrent/latest/webtorrent.min.js)脚本。

```html
<script src="webtorrent.min.js"></script>
```

这给`window`对象中，提供了一个`WebTorrent`函数。

### Browserify

WebTorrent 也与[browserify](http://browserify.org/)很搭，让你使用[node.js](http://nodejs.org/)的`require()`样式，组织您的浏览器代码，并加载[npm](https://npmjs.org/)安装的软件包。

```
npm install webtorrent
```

然后，像这样用`WebTorrent`：

```js
var WebTorrent = require('webtorrent');
```

## 快例子

### 下载一个 torrent (在浏览器)

```js
var WebTorrent = require('webtorrent');

var client = new WebTorrent();

// Sintel, 一部免费，好的电影
var torrentId =
  'magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent';

client.add(torrentId, function(torrent) {
  // Torrents 可以包含许多文件（files）. 让我们使用 .mp4 文件
  var file = torrent.files.find(function(file) {
    return file.name.endsWith('.mp4');
  });

  // 通过添加到 DOM , 展示该文件。
  // 支持 video, audio, image 文件, 还有更多!
  file.appendTo('body');
});
```

这支持视频，音频，图像，PDF，Markdown，[和更多][render-media]，开箱即用。还有其他方法，可以直接访问文件内容，包括 node-样式的流媒体，Buffer 或 Blob URL。

视频和音频内容可以流式传输，即在下载完整文件之前，开始播放。播种工作也是如此 - WebTorrent 根据需要，从网络中，动态获取所需的 torrent 片段。

### 创建一个 torrent(种子) 和 播种 (在浏览器)

```js
var dragDrop = require('drag-drop');
var WebTorrent = require('webtorrent');

var client = new WebTorrent();

// 当用户把文件，拖到浏览器，会创建一个新的 torrent 并开始播种！
dragDrop('body', function(files) {
  client.seed(files, function(torrent) {
    console.log('Client is seeding ' + torrent.magnetURI);
  });
});
```

这个例子使用了[`drag-drop`][drag-drop]包，让 HTML5 拖放(Drag 和 Drop) API 更容易使用。

**注意：**如果您不使用 browserify，请使用独立文件[`dragdrop.min.js`](https://raw.githubusercontent.com/feross/drag-drop/master/dragdrop.min.js)。这导出一个`DragDrop`函数，到`window`。

### 下载和保存 一个 torrent (Node.js)

```js
var WebTorrent = require('webtorrent');

var client = new WebTorrent();

var magnetURI = 'magnet: ...';

client.add(magnetURI, {path: '/path/to/folder'}, function(torrent) {
  torrent.on('done', function() {
    console.log('torrent download finished');
  });
});
```

### 完整的网页示例

寻找更完整的例子？不用到处找啦！此 HTML 示例具有表单输入，用户可以粘贴，磁力链接，并通过 WebTorrent 开始下载。

最重要的是，它是一个单独的 HTML 页面，低于 70 行！

如果 torrent 包含图像，视频，音频或其他可播放文件（使用支持的编解码器），则即使在下载完整内容之前，它们也能添加到 DOM ，并进行流式传输。

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>
      使用 WebTorrent 协议 (BitTorrent ^ WebRTC) 下载文件.
    </h1>

    <form>
      <label for="torrentId">磁力链接下载 </label>
      <input
        name="torrentId"
        ,
        placeholder="magnet:"
        value="magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent"
      />
      <button type="submit">下载</button>
    </form>

    <h2>记录</h2>
    <div class="log"></div>

    <!-- Include the latest version of WebTorrent -->
    <script src="https://cdn.jsdelivr.net/webtorrent/latest/webtorrent.min.js"></script>

    <script>
      var client = new WebTorrent();

      client.on('error', function(err) {
        console.error('ERROR: ' + err.message);
      });

      document.querySelector('form').addEventListener('submit', function(e) {
        e.preventDefault(); // 阻止网页刷新

        var torrentId = document.querySelector('form input[name=torrentId]')
          .value;
        log('Adding ' + torrentId);
        client.add(torrentId, onTorrent);
      });

      function onTorrent(torrent) {
        log('获得 torrent 元信息!');
        log(
          'Torrent info hash: ' +
            torrent.infoHash +
            ' ' +
            '<a href="' +
            torrent.magnetURI +
            '" target="_blank">[Magnet URI]</a> ' +
            '<a href="' +
            torrent.torrentFileBlobURL +
            '" target="_blank" download="' +
            torrent.name +
            '.torrent">[Download .torrent]</a>'
        );

        // 每5秒，打印下载进度
        var interval = setInterval(function() {
          log('Progress: ' + (torrent.progress * 100).toFixed(1) + '%');
        }, 5000);

        torrent.on('done', function() {
          log('Progress: 100%');
          clearInterval(interval);
        });

        // 把所有文件，渲染进 DOM
        torrent.files.forEach(function(file) {
          file.appendTo('.log');
          log(
            '(Blob URLs 从服务器加载完成后，才能工作. "http//localhost" 可以. "file://" 不行.)'
          );
          file.getBlobURL(function(err, url) {
            if (err) return log(err.message);
            log('File 完成.');
            log(
              '<a href="' + url + '">下载完整的文件: ' + file.name + '</a>'
            );
          });
        });
      }

      function log(str) {
        var p = document.createElement('p');
        p.innerHTML = str;
        document.querySelector('.log').appendChild(p);
      }
    </script>
  </body>
</html>
```

### HTML 示例：状态显示 UI

这个完整的 HTML 示例，模仿了[webtorrent.io](https://webtorrent.io)主页的UI。它下载了[sintel.torrent](https:./torrents.zh.md/sintel.torrent)文件，在浏览器中，流式传输并向用户输出一些统计信息（对端(可供给的网点)，进度，剩余时间，速度...）。

你现在可以在[CodePen](http://codepen.io/yciabaud/full/XdOeWM/)试试，看看它的样子，玩玩它！

随意更换`torrentId`，换成其他 torrent 文件，或磁力链接，但请记住，浏览器只能下载，由 WebRTC 对端（web 对端）播种的种子。使用[WebTorrent 桌面程序](https:./desktop.zh.md)要么[Instant.io](https://instant.io)，将种子(torrent)，播种到 WebTorrent 网络。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebTorrent 视频播放器</title>
    <style>
      #output video {
        width: 100%;
      }
      #progressBar {
        height: 5px;
        width: 0%;
        background-color: #35b44f;
        transition: width 0.4s ease-in-out;
      }
      body.is-seed .show-seed {
        display: inline;
      }
      body.is-seed .show-leech {
        display: none;
      }
      .show-seed {
        display: none;
      }
      #status code {
        font-size: 90%;
        font-weight: 700;
        margin-left: 3px;
        margin-right: 3px;
        border-bottom: 1px dashed rgba(255, 255, 255, 0.3);
      }

      .is-seed #hero {
        background-color: #154820;
        transition: 0.5s 0.5s background-color ease-in-out;
      }
      #hero {
        background-color: #2a3749;
      }
      #status {
        color: #fff;
        font-size: 17px;
        padding: 5px;
      }
      a:link,
      a:visited {
        color: #30a247;
        text-decoration: none;
      }
    </style>
  </head>
  <body>
    <div id="hero">
      <div id="output">
        <div id="progressBar"></div>
        <!-- The video player will be added here -->
      </div>
      <!-- Statistics -->
      <div id="status">
        <div>
          <span class="show-leech">下载中 </span>
          <span class="show-seed">播种中 </span>
          <code>
            <!-- Informative link to the torrent file -->
            <a id="torrentLink" href="https:./torrents.zh.md/sintel.torrent"
              >sintel.torrent</a
            >
          </code>
          <span class="show-leech"> 从 </span>
          <span class="show-seed"> 到 </span>
          <code id="numPeers">0 对端</code>.
        </div>
        <div>
          <code id="downloaded"></code>
          of <code id="total"></code> — <span id="remaining"></span><br />
          &#x2198;<code id="downloadSpeed">0 b/s</code> / &#x2197;<code
            id="uploadSpeed"
            >0 b/s</code
          >
        </div>
      </div>
    </div>
    <!-- Include the latest version of WebTorrent -->
    <script src="https://cdn.jsdelivr.net/webtorrent/latest/webtorrent.min.js"></script>

    <!-- Moment is used to show a human-readable remaining time -->
    <script src="http://momentjs.com/downloads/moment.min.js"></script>

    <script>
      var torrentId = 'https://webtorrent.io/torrents/sintel.torrent';

      var client = new WebTorrent();

      // HTML elements
      var $body = document.body;
      var $progressBar = document.querySelector('#progressBar');
      var $numPeers = document.querySelector('#numPeers');
      var $downloaded = document.querySelector('#downloaded');
      var $total = document.querySelector('#total');
      var $remaining = document.querySelector('#remaining');
      var $uploadSpeed = document.querySelector('#uploadSpeed');
      var $downloadSpeed = document.querySelector('#downloadSpeed');

      // 下载种子
      client.add(torrentId, function(torrent) {
        // Torrents 可以包含许多文件（files）. 让我们使用 .mp4 文件
        var file = torrent.files.find(function(file) {
          return file.name.endsWith('.mp4');
        });

        // 在浏览器，流式播放文件
        file.appendTo('#output');

        // 触发 统计 刷新
        torrent.on('done', onDone);
        setInterval(onProgress, 500);
        onProgress();

        // 统计
        function onProgress() {
          // Peers
          $numPeers.innerHTML =
            torrent.numPeers + (torrent.numPeers === 1 ? ' peer' : ' peers');

          // 进度
          var percent = Math.round(torrent.progress * 100 * 100) / 100;
          $progressBar.style.width = percent + '%';
          $downloaded.innerHTML = prettyBytes(torrent.downloaded);
          $total.innerHTML = prettyBytes(torrent.length);

          // 剩余时间
          var remaining;
          if (torrent.done) {
            remaining = 'Done.';
          } else {
            remaining = moment
              .duration(torrent.timeRemaining / 1000, 'seconds')
              .humanize();
            remaining =
              remaining[0].toUpperCase() +
              remaining.substring(1) +
              ' 还需时间.';
          }
          $remaining.innerHTML = remaining;

          // Speed rates
          $downloadSpeed.innerHTML = prettyBytes(torrent.downloadSpeed) + '/s';
          $uploadSpeed.innerHTML = prettyBytes(torrent.uploadSpeed) + '/s';
        }
        function onDone() {
          $body.className += ' is-seed';
          onProgress();
        }
      });

      // 人类可读字节工具
      function prettyBytes(num) {
        var exponent,
          unit,
          neg = num < 0,
          units = ['B', 'kB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'];
        if (neg) num = -num;
        if (num < 1) return (neg ? '-' : '') + num + ' B';
        exponent = Math.min(
          Math.floor(Math.log(num) / Math.log(1000)),
          units.length - 1
        );
        num = Number((num / Math.pow(1000, exponent)).toFixed(2));
        unit = units[exponent];
        return (neg ? '-' : '') + num + ' ' + unit;
      }
    </script>
  </body>
</html>
```

## 更多文档

看看[API 文档](./api.zh.md)和[FAQ](./faq.zh.md)，里面有更多细节。

[render-media]: https://github.com/feross/render-media/blob/master/index.js#L12-L20
[drag-drop]: https://npmjs.com/package/drag-drop
