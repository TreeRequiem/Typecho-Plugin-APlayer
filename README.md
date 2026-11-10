> 基于 [mikusaa/Typecho-Plugin-APlayer](https://github.com/mikusaa/Typecho-Plugin-APlayer) fork，MIT License，改动见 [CHANGELOG.md](CHANGELOG.md)

<p align="center">
<img src="https://user-images.githubusercontent.com/2666735/30651452-58ae6c88-9deb-11e7-9e13-6beae3f6c54c.png" alt="Meting">
</p>

 > 在 Typecho 中使用 APlayer 播放在线音乐吧～
 > [仓库地址](https://github.com/TreeRequiem/Typecho-Plugin-APlayer)<br>
 > [Releases](https://github.com/TreeRequiem/Typecho-Plugin-APlayer/releases)

## 介绍
  1. 支持国内五大音乐平台（网易云、QQ、酷狗、百度、酷我）的单曲/专辑/歌单播放
  2. 简单快捷，复制音乐详情页面网址，后台自动生成播放代码
  3. 前端 APlayer，后端 Meting 及时更新，保证兼容性及 API 高可用性
  4. 支持 MySql、SQLite 数据库
  5. **支持 Redis, Memcached 缓存**
  6. 支持自定义歌曲播放
  7. **自定义 API 支持**

## 声明
本作品仅供个人学习研究使用，请勿将其用作商业用途。  
**!!切勿使用本插件代码下载版权保护音乐!!**

## 安装
  1. 在仓库 Releases 页面下载压缩包
  2. 上传到 /usr/plugins 目录
  3. **修改文件夹名为 Meting**
  4. 后台启用插件

## 使用
在文章编辑页面，点击编辑器上的 **音乐图标** 按钮，在弹出的窗口中输入音乐地址（见支持列表），最后点击确定即可

## 自定义播放器参数

默认情况下插件会读取后台配置面板里的全局默认值，同时 **所有 APlayer 公开参数** 都可以直接写在 `[Meting]` 标签上进行**内联覆盖**。

### 写法规则

短代码中的属性名需使用 **kebab-case**（连字符分隔），例如 APlayer 的 `listFolded` 写为 `list-folded`、`storageName` 写为 `storage-name`。布尔值写 `"true"` 或 `"false"` 字符串即可。

### 示例

```
[Meting order="random" loop="one" mini="true" list-folded="true" volume="0.5"]
[Music server="netease" id="13891298296" type="playlist" /]
[/Meting]
```

上面这条短代码将此播放器的**播放顺序**改为随机、**循环方式**改为单曲循环、开启**迷你模式**、**列表默认折叠**、**默认音量**调为 0.5，其他未声明的参数（如 theme、preload 等）仍然使用后台配置的全局默认值。

### 参数清单

下表列出常用的 APlayer 参数。标记 **✅** 表示该参数可在插件后台配置面板设置全局默认值。

| 参数（kebab-case） | 后台可设默认 | 说明 | 示例 |
|---|---|---|---|
| `theme` | ✅ | 主题颜色 | `theme="#FADFA3"` |
| `preload` | ✅ | 预加载方式：`auto` / `none` / `metadata` | `preload="metadata"` |
| `autoplay` | ✅ | 自动播放（移动端浏览器通常会忽略） | `autoplay="true"` |
| `order` | ✅ | 播放顺序：`list` / `random` | `order="random"` |
| `list-max-height` | ✅ | 播放列表最大高度 | `list-max-height="200px"` |
| `mini` | ✅ | 迷你模式（与吸底模式冲突） | `mini="true"` |
| `fixed` | ✅ | 吸底模式（与迷你模式冲突） | `fixed="true"` |
| `loop` | ✅ | 循环方式：`all` / `one` / `none` | `loop="one"` |
| `list-folded` | ✅ | 列表默认折叠 | `list-folded="true"` |
| `volume` | ✅ | 默认音量，范围 0–1 | `volume="0.5"` |
| `lrc-type` | ❌ | 歌词方式（0–3），默认 3 | `lrc-type="1"` |
| `mutex` | ❌ | 多播放器互斥，默认 `true` | `mutex="false"` |
| `storage-name` | ❌ | localStorage 存储键名 | `storage-name="my-player"` |

> 未列入上表但 APlayer 官方支持的参数（如 `container` 之外的所有配置项）同样可以在 `[Meting]` 标签上内联使用，插件和 MetingJS 会自动透传。

### 优先级

1. **短代码内联**（写在 `[Meting]` 标签上的属性）
2. **插件后台配置面板**（全局默认值）
3. **前端 MetingJS / APlayer 内置默认值**

## 支持列表
网易云音乐 http://music.163.com
 - 单曲 http://music.163.com/#/song?id=424474911
 - 专辑 http://music.163.com/#/album?id=34808540
 - 歌手 http://music.163.com/#/artist?id=3681
 - 歌单 http://music.163.com/#/playlist?id=436843836
 - 榜单 http://music.163.com/#/discover/toplist?id=60198

QQ 音乐 https://y.qq.com
 - 单曲 https://y.qq.com/n/yqq/song/000jDQWP4JiB3y.html
 - 专辑 https://y.qq.com/n/yqq/album/003rytri2FHG3V.html
 - 歌手 https://y.qq.com/n/yqq/singer/003Nz2So3XXYek.html
 - 歌单 https://y.qq.com/n/yqq/playlist/1144188779.html

酷狗音乐 http://www.kugou.com
 - 单曲 http://www.kugou.com/song/#hash=09E8DE70A24C97B92A29F6A19F3528A2
 - 专辑 http://www.kugou.com/yy/album/single/1645030.html
 - 歌手 http://www.kugou.com/yy/singer/home/3520.html
 - 歌单 http://www.kugou.com/yy/special/single/119859.html

百度音乐 http://music.baidu.com/
 - 单曲 http://music.baidu.com/song/268275324
 - 专辑 http://music.baidu.com/album/268275533
 - 歌手 http://music.baidu.com/artist/1219
 - 歌单 http://music.baidu.com/songlist/364201689

酷我音乐 https://www.kuwo.cn
 - 单曲 https://www.kuwo.cn/play_detail/156483846
 - 专辑 https://www.kuwo.cn/album_detail/14525256
 - 歌手 https://www.kuwo.cn/singer_detail/431
 - 歌单 https://www.kuwo.cn/playlist_detail/3130806604

## FAQ

<details><summary>PJAX 页面切换问题？</summary><br>

当前版本默认使用 `<meting-js>` Custom Element 渲染播放器。  
在常见的 PJAX 场景下，新页面内容插入后会自动初始化播放器，旧节点移除时也会自动销毁，一般**不需要**再额外添加 `loadMeting()` 一类的重载函数。

如果你的主题对 PJAX 做了额外的 DOM 接管，或自行阻断了自定义元素的正常生命周期，再根据主题行为补充自定义回调即可。

</details>


<details><summary>不支持混合歌单？</summary><br>

由于 2.x 版本重写了实现方式，旧的混合歌单将不再支持，建议通过各音乐平台创建歌单的方式添加。

</details>


<details><summary>升级问题？</summary><br>

目前插件支持在设置页面差量升级，但由于某些版本做了较大调整，可能造成插件无法使用，可以禁用插件再启用修复。

</details>


更多问题可以通过 GitHub Issues 页面提交，或者通过 Telegram、邮件向我反馈

## LICENSE
Typecho-Plugin-APlayer is under the MIT license.
