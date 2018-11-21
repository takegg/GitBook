# youtube-dl

<a href="https://github.com/rg3/youtube-dl">github仓库</a>

```shell
youtube-dl [OPTIONS] URL [URL...]
```
### 选项
```
-i, --ignore-errors                 当下载错误继续下载，例如列表中的不可用视频
```
### 视频选择

```
--playlist-start NUMBER             要播放的播放列表视频（默认为1）

--playlist-end NUMBER               播放列表视频结束（默认为最后）

--playlist-items ITEM_SPEC          要下载的播放列表视频项目。 如果要下载播放列表中索引为1,2,5,8的视频，请指定播放列表中用逗号分隔的视频索引，如：“ - playlist-items 1,2,5,8”。 您可以指定范围：“ - playlist-items 1-3,7,10-13”，它将下载索引1,2,3,7,10,11,12和13的视频。

--match-title REGEX                 仅下载匹配的标题（正则表达式或无壳子字符串）

--reject-title REGEX                跳过下载匹配的标题（正则表达式或无壳子串）

--max-downloads NUMBER              下载NUMBER个文件后中止

。。。。。。。等
```
### 下载选项：
```shell
-f, --format FORMAT                 视频格式代码，请参阅“格式化”选择“所有信息

--all-formats                       下载所有可用的视频格式

--prefer-free-formats               除非特定，否则更喜欢免费视频格式一个是要求的

-F, --list-formats                  列出所有可用的格式视频

--youtube-skip-dash-manifest        不要下载DASH清单和YouTube视频的相关数据

--merge-output-format FORMAT        如果需要合并（例如bestvideo + bestaudio），输出到给定容器格式。其中一个mkv，mp4，ogg，webm，flv。如果不需要合并，则忽略
```

### 字幕选项：

```shell
--write-sub                         写字幕文件

--write-auto-sub                    写自动生成的字幕文件（仅限YouTube）

--all-subs                          下载视频所有可用的字幕

--list-subs                         列出视频的所有可用字幕

--sub-format FORMAT                 字幕格式，接受格式偏好，例如：“srt”或“驴/ SRT /最佳”

--sub-lang LANGS                    要下载的字幕语言（可选）用逗号分隔，使用--list-subs 可用语言标签的
```

### 后处理选项：

```
-x, --extract-audio                 将视频文件转换为纯音频文件（需要ffmpeg或avconv和ffprobe或avprobe）

--audio-format FORMAT               指定音频格式：“best”，“aac”，“flac”，“mp3”，“m4a”，“opus”，“vorbis”或“WAV”;默认情况下“最好”;没有效果-X
```

### 常用命令

```shell
youtube-dl --merge-output-format mp4 [url]
```