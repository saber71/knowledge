# ffmpeg是什么

多媒体框架，能够编解码、转码、复用、分离、流式传输、过滤、播放几乎所有格式的音视频格式

# js的ffmpeg库

fluent-ffmpeg，适用于node环境

``` javascript
// 示例代码
const ffmpeg = require("fluent-ffmpeg");

function convertMp4ToMp3(inputPath, outputPath) {
  return new Promise((resolve, reject) => {
    ffmpeg(inputPath)
      .output(outputPath)
      .audioCodec("libmp3lame") // 使用 MP3 编解码器
      .on("end", () => {
        console.log("转换完成");
        resolve();
      })
      .on("error", (err) => {
        console.error("转换错误:", err);
        reject(err);
      })
      .run();
  });
}

const inputVideoPath = "./source/天梯.mp4"; // MP4 文件路径
const outputAudioPath = "./output/天梯.mp3"; // 输出 MP3 文件路径

convertMp4ToMp3(inputVideoPath, outputAudioPath)
  .then(() => console.log("MP4 转 MP3 成功"))
  .catch((err) => console.error("MP4 转 MP3 失败:", err));

```