# webtorrent/webtorrent [![explain]][source] [![translate-svg]][translate-list]

<!-- [![size-img]][size] -->

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/Source-Explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list
[size-img]: https://packagephobia.now.sh/badge?p=Name
[size]: https://packagephobia.now.sh/result?p=Name

「 desc 」

[中文](./readme.md) | [english](https://github.com/webtorrent/webtorrent)

---

## 校对 🀄️

<!-- doc-templite START generated -->
<!-- repo = 'webtorrent/webtorrent' -->
<!-- commit = 'true' -->
<!-- time = 'true' -->

<!-- doc-templite END generated -->

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

### 目录

<!-- START doctoc -->
<!-- END doctoc -->

# Get Started with WebTorrent

**WebTorrent**是第一个在该工作的 torrent 客户端**浏览器**。它很容易上手！

## Install

要开始使用 WebTorrent，只需包含[`webtorrent.min.js`](https://cdn.jsdelivr.net/webtorrent/latest/webtorrent.min.js)您网页上的脚本。

```html
<script src="webtorrent.min.js"></script>
```

这提供了一个`WebTorrent`功能上`window`宾语。

### Browserify

WebTorrent 也很适合[browserify](http://browserify.org/)，让你使用[node.js](http://nodejs.org/)样式`require()`组织您的浏览器代码，并加载安装的软件包[npm](https://npmjs.org/)。

```
npm install webtorrent
```

然后用`WebTorrent`像这样：

```js
var WebTorrent = require('webtorrent');
```

## Quick Examples

### Downloading a torrent (in the browser)

```js
var WebTorrent = require('webtorrent');

var client = new WebTorrent();

// Sintel, a free, Creative Commons movie
var torrentId =
  'magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent';

client.add(torrentId, function(torrent) {
  // Torrents can contain many files. Let's use the .mp4 file
  var file = torrent.files.find(function(file) {
    return file.name.endsWith('.mp4');
  });

  // Display the file by adding it to the DOM.
  // Supports video, audio, image files, and more!
  file.appendTo('body');
});
```

这支持视频，音频，图像，PDF，Markdown，[和更多][render-media]，开箱即用。还有其他方法可以直接访问文件内容，包括节点样式的流，缓冲区或 Blob URL。

视频和音频内容可以流式传输，即在下载完整文件之前开始播放。寻求工作也是如此 - WebTorrent 根据需要动态地从网络中获取所需的 torrent 片段。

### Creating a new torrent and seed it (in the browser)

```js
var dragDrop = require('drag-drop');
var WebTorrent = require('webtorrent');

var client = new WebTorrent();

// When user drops files on the browser, create a new torrent and start seeding it!
dragDrop('body', function(files) {
  client.seed(files, function(torrent) {
    console.log('Client is seeding ' + torrent.magnetURI);
  });
});
```

这个例子使用了[`drag-drop`][drag-drop]包，使 HTML5 拖放 API 更容易使用。

**注意：**如果您不使用 browserify，请使用独立文件[`dragdrop.min.js`](https://raw.githubusercontent.com/feross/drag-drop/master/dragdrop.min.js)。这导出一个`DragDrop`功能`window`。

### Download and save a torrent (in Node.js)

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

### Complete HTML page example

寻找更完整的例子？别再看了！此 HTML 示例具有表单输入，用户可以粘贴磁力链接并通过 WebTorrent 开始下载。

最重要的是，它是一个单独的 HTML 页面，低于 70 行！

如果 torrent 包含图像，视频，音频或其他可播放文件（使用支持的编解码器），则即使在下载完整内容之前，它们也会添加到 DOM 并进行流式传输。

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>
      Download files using the WebTorrent protocol (BitTorrent over WebRTC).
    </h1>

    <form>
      <label for="torrentId">Download from a magnet link: </label>
      <input
        name="torrentId"
        ,
        placeholder="magnet:"
        value="magnet:?xt=urn:btih:08ada5a7a6183aae1e09d831df6748d566095a10&dn=Sintel&tr=udp%3A%2F%2Fexplodie.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Ftracker.empire-js.us%3A1337&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337&tr=wss%3A%2F%2Ftracker.btorrent.xyz&tr=wss%3A%2F%2Ftracker.fastcast.nz&tr=wss%3A%2F%2Ftracker.openwebtorrent.com&ws=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2F&xs=https%3A%2F%2Fwebtorrent.io%2Ftorrents%2Fsintel.torrent"
      />
      <button type="submit">Download</button>
    </form>

    <h2>Log</h2>
    <div class="log"></div>

    <!-- Include the latest version of WebTorrent -->
    <script src="https://cdn.jsdelivr.net/webtorrent/latest/webtorrent.min.js"></script>

    <script>
      var client = new WebTorrent();

      client.on('error', function(err) {
        console.error('ERROR: ' + err.message);
      });

      document.querySelector('form').addEventListener('submit', function(e) {
        e.preventDefault(); // Prevent page refresh

        var torrentId = document.querySelector('form input[name=torrentId]')
          .value;
        log('Adding ' + torrentId);
        client.add(torrentId, onTorrent);
      });

      function onTorrent(torrent) {
        log('Got torrent metadata!');
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

        // Print out progress every 5 seconds
        var interval = setInterval(function() {
          log('Progress: ' + (torrent.progress * 100).toFixed(1) + '%');
        }, 5000);

        torrent.on('done', function() {
          log('Progress: 100%');
          clearInterval(interval);
        });

        // Render all files into to the page
        torrent.files.forEach(function(file) {
          file.appendTo('.log');
          log(
            '(Blob URLs only work if the file is loaded from a server. "http//localhost" works. "file://" does not.)'
          );
          file.getBlobURL(function(err, url) {
            if (err) return log(err.message);
            log('File done.');
            log(
              '<a href="' + url + '">Download full file: ' + file.name + '</a>'
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

### HTML example with status showing UI

这个完整的 HTML 示例模仿了 UI 的 UI[webtorrent.io](https://webtorrent.io)主页。它下载了[sintel.torrent](https://webtorrent.io/torrents/sintel.torrent)文件，在浏览器中流式传输并向用户输出一些统计信息（同级，进度，剩余时间，速度......）。

你现在可以尝试一下[CodePen](http://codepen.io/yciabaud/full/XdOeWM/)看看它的样子，玩弄它！

随意更换`torrentId`与其他 torrent 文件或磁链接，但请记住，浏览器只能下载由 WebRTC 对等（web 对等）播种的种子。使用[WebTorrent Desktop](https://webtorrent.io/desktop)要么[Instant.io](https://instant.io)将种子播种到 WebTorrent 网络。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>WebTorrent video player</title>
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
          <span class="show-leech">Downloading </span>
          <span class="show-seed">Seeding </span>
          <code>
            <!-- Informative link to the torrent file -->
            <a
              id="torrentLink"
              href="https://webtorrent.io/torrents/sintel.torrent"
              >sintel.torrent</a
            >
          </code>
          <span class="show-leech"> from </span>
          <span class="show-seed"> to </span>
          <code id="numPeers">0 peers</code>.
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

      // Download the torrent
      client.add(torrentId, function(torrent) {
        // Torrents can contain many files. Let's use the .mp4 file
        var file = torrent.files.find(function(file) {
          return file.name.endsWith('.mp4');
        });

        // Stream the file in the browser
        file.appendTo('#output');

        // Trigger statistics refresh
        torrent.on('done', onDone);
        setInterval(onProgress, 500);
        onProgress();

        // Statistics
        function onProgress() {
          // Peers
          $numPeers.innerHTML =
            torrent.numPeers + (torrent.numPeers === 1 ? ' peer' : ' peers');

          // Progress
          var percent = Math.round(torrent.progress * 100 * 100) / 100;
          $progressBar.style.width = percent + '%';
          $downloaded.innerHTML = prettyBytes(torrent.downloaded);
          $total.innerHTML = prettyBytes(torrent.length);

          // Remaining time
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
              ' remaining.';
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

      // Human readable bytes util
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

## More Documentation

看看[API Documentation](//webtorrent.io/docs)和[FAQ](//webtorrent.io/faq)更多细节。

[render-media]: https://github.com/feross/render-media/blob/master/index.js#L12-L20
[drag-drop]: https://npmjs.com/package/drag-drop
