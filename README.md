# P2P-hls

**P2P hls** is a JavaScript library based on hls.js to implement video traffic delivery over P2P in web browsers.

It allows creating Peer-to-Peer network (also called P2P CDN or P2PTV) for traffic sharing between users (peers) that are watching the same video stream live or VOD over HLS.

Powered by hls.js, it can play HLS on any platform with many popular HTML5 players.

It significantly reduces traditional CDN traffic and cost while delivering video streams to more users.

**Save Your Bandwidth using WebRTC.**

## Useful Demo

- [Demo](https://webp2p.augok.com/p2pdemo/)

**Example**

https://webp2p.augok.com/p2pdemo/?url=https://m3u8.link.address/video.m3u8


## Quick Start

Download the latest release and load the JavaScript library.

Add these tags to your document's `<head>`:

```html
<script src="your filepath/../p2pl.js"></script>
<script src="your filepath/../p2ph.js"></script>
<script src="your filepath/../p2phls.js"></script>
```

Then there's a free, CDN hosted version of hls.js that anyone can use. Add these tags to your document's `<head>`:

```html
<script src="https://unpkg.com/hls.min@0.0.2/index.js"></script>
```

## Example by DPlayer

```html
<script src="your filepath/../p2pl.js"></script>
<script src="your filepath/../p2ph.js"></script>
<script src="your filepath/../p2phls.js"></script>
<script src="https://unpkg.com/hls.min@0.0.2/index.js"></script>
<!-- unpkg : use the latest version of DPlayer.js -->
<script src="https://unpkg.com/dplayer/dist/DPlayer.min.js"></script>
```

```js
// url is link address.
var p2phls = new P2Phls(url);

var player = new DPlayer({
    container: document.getElementById('video'),
    autoplay: true,
    preload: 'auto',
    video: {
        url: url,
        type: 'customHls',
        customType: {
            'customHls': function(video, player) {
                var hls = new Hls({
                    liveSyncDurationCount: 7,
                    loader: p2phls.getLoader()
                });
                p2phls.initHlsPlayer(hls);

                hls.loadSource(video.src);
                hls.attachMedia(video);
            }
        }
    }
});
```

## API

**isP2P()**

Determine whether to support P2P.

```js
// p2phls is new P2Phls(url) object
p2phls.isP2P()
// return true or false
```

**isHls()**

Determine whether to support Hls.

```js
// p2phls is new P2Phls(url) object
p2phls.isHls()
// return true or false
```

## Event

**bytechange**

Monitor traffic download btye.

```js
// p2phls is new P2Phls(url) object
p2phls.on('bytechange', function(data){
    var httpMb = data.http; // http traffic download btyes
    var p2pMb = data.p2p; // p2p traffic download btyes
});
```

**peers**

Monitor P2P peers connections.

```js
// p2phls is new P2Phls(url) object
p2phls.on('peers', function(num,peer){
    num; //peers num
    peer; // peer detail object
});
```

**See p2pdemo for more...**

## Contact Us

Telegram: @augok009








