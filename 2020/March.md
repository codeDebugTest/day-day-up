# 三月

## 10
video标签中的播放是异步地，video.play()返回一个promise.
背景：
```javascript
  <video id=“video” preload="none" src="http://xxxx.mp4"></video>
  <script>
     video.play();
     video.pause();
  </script>
```
上面的代码在chrome DevTools 会看到错误信息：**Uncaught (in promise) DOMException: The play() request was interrupted by a call to pause().**
  
原因：由于 preload=“none”，调用 video.play() 不会立即播放，而是先加载视频资源。当然 video.play()本身也是返回一个promise对象, 如果播放成功，则调用resolve 同时触发播放事件，如果播放失败则调用reject。
上面的代码相当于：
1. video.play(); 异步加载视频资源
2. video.pause(); 中断加载，因为视频尚未ready
3. video.play(); 由于 video.pause()中断播放，返回promise reject。
由于没有处理 video.play 的 promise reject，所以出现了上面的错误。
**注意： video.pause()不是唯一中断视频的方式，例如：通过 video.src='' 重置播放状态一样可以中断播放, 或者视频资源不存在**
  
修复：
``` javascript
    const playPromise = video.play();
    playPromise.then(_ => {
      // Automatic playback started!
      // Show playing UI.
      ...
      // We can now safely pause video...
      video.pause();
    })
    .catch(error => {
      // Auto-play was prevented
      // Show paused UI.
    });
```

扩展一：**怎样稍后播放视频？**
```javascript
<video id="video"></video>
<button id="button"></button>
<script>
  button.addEventListener('click', onButtonClick);

  function onButtonClick() {
    // This will allow us to play video later...
    video.load();
    fetchVideoAndPlay();
  }

  function fetchVideoAndPlay() {
    fetch('https://example.com/file.mp4')
    .then(response => response.blob())
    .then(blob => {
      video.srcObject = blob;
      return video.play();
    })
    .then(_ => {
      // Video playback started ;)
    })
    .catch(e => {
      // Video playback failed ;(
    })
  }
</script>
```
扩展二：包含了<source>标签的<video> play() promise 从不会reject
```javascript
 <video src="not-existing-video.mp4"></video> // promise reject
 <video><source src="not-existing-video.mp4" type='video/mp4'></video> // never reject, 除非没有有效资源
```

