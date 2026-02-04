<div align="center">
  <img src="./frontend/assets/logo.svg" width="56px"/>
  <h1>StreamUI</h1>
</div>

### Overview

一个极简轻量的视频流媒体管理平台

> StreamUI 中 Stream 取自 [ZLMediaKit](https://github.com/ZLMediaKit/ZLMediaKit) 流概念，UI 取自 [Layui](https://github.com/layui/layui)。整体设计以蓝绿色（`#16baaa`）为主色调，秉持 “简洁、易用、可扩展” 的理念，在代码复杂度与功能实现之间不断权衡取舍，执着追求极简之美。


### Features

- 支持 RTSP/RTMP/HLS/WebRTC/RTP/GB28181 等主流协议的拉流推流接入

- 支持 ONVIF 设备识别

- 支持分发 RTSP/WebRTC/RTMP/FLV/HLS/HLS-fMP4/HTTP-TS/HTTP-fMP4 等协议

- 支持多屏播放

- 支持流本地录制、回放、下载、自动清理，支持事件录制（事件发生前 n 秒+事件发生后 n 秒）

- 🚧 支持 GB28181 接入/级联（正在实现中 ...）


### Quick Start

此项目推荐使用Docker Compose部署。

```shell
cd ./docker
docker compose up -d
```

运行后，打开浏览器并转到`http://{你的服务器IP}:10800`登录。

默认密码为`streamui`，你可以在 [login.html](./frontend/login.html) 中更改它。

如果你更改设置并希望更改生效，只需使用以下命令重新启动服务：

```shell
docker compose restart
```

### Tips

首次启动后，建议先根据业务需要修改配置再重启使用

- 考虑开启按需转发，优点是节省带宽，缺点是第一个观众观看时，需要等待转发流启动

- 考虑关掉不需要转发的协议，比如不需要分发 RTMP 协议，就关掉 RTMP 转发

- 考虑开启 faststart，优点是播放时可以快速 seek，缺点是录制时需要多占用一些存储空间

- 考虑增大 GOP 缓存，优点是播放平滑，录制事件视频回溯时间变长，缺点是增大内存占用


更多选项深入研究请参考 ZLMediaKit 的 [配置说明](https://github.com/ZLMediaKit/ZLMediaKit/tree/master/conf)


### Snapshots

<img src="./snapshots/login.png" alt="wall" style="zoom:33%;" />

<img src="./snapshots/home.png" alt="home" style="zoom: 33%;" />

### Repo Structure

StreamUI 追求极简实现，前端未采用 Vue、React 等重量级框架，后端也避开了功能繁杂的 Java Spring 体系，转而选用轻量级的 Layui 与 FastAPI 组合。整体架构简洁清晰，易于理解和二次开发。


```bash
├── backend
│   ├── main.py  # 主程序入口
│   ├── onvif  # ONVIF 设备识别与云台控制
│   ├── scheduler.py  # 定时任务
│   └── utils.py  # 工具函数  
│
├── frontend
│   ├── assets  # 静态资源
│   ├── index.html  # 主页面
│   ├── login.html  # 登录页面
│   └── pages
│       ├── api-docs.html  # 接口文档
│       ├── home.html  # 首页概览
│       ├── playback.html  # 录像回放
│       ├── pull-stream.html  # 主动拉流
│       ├── settings.html  # 基础配置
│       ├── stream-push.html  # 被动推流
│       └── wall.html  # 分屏展示
```

### Thanks

- [ZLMediaKit](https://github.com/ZLMediaKit/ZLMediaKit)
- [Layui](https://github.com/layui/layui)
- [FastAPI](https://fastapi.tiangolo.com/)

🤗 ZLMediaKit https://github.com/ZLMediaKit/ZLMediaKit has included this project

### License

StreamUI is licensed under the [MIT License](./LICENSE)