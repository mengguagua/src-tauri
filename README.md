## tauri使用

### 背景

有现成的前端项目，比如react，vue此类，要打包成pc客户端

官网文档：https://tauri.app/zh-cn/v1/guides/getting-started/setup/integrate

### 打包步骤

#### 系统(macOS)安装依赖

需要安装 CLang 和 macOS 开发依赖项；再安装 Rust

```shell
# 一般操作系统都默认安装过
xcode-select --install
# 要在 macOS 上安装 Rust
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

#### 下载tauri脚手架

```shell
# 在已有项目目录下执行即可
npm install --save-dev @tauri-apps/cli
```

在现有项目增加指令，以构建tauri项目
```json
"scripts": {
  "tauri": "tauri"
}
```

#### 创建tauri项目

```shell
# 按各项提示创建即可，后面可以在配置文件修改
npm run tauri init
```

#### 和现有项目结合

将创建的tauri项目，复制到以下结构

```
│── package.json
│── public
│   ╰── index.html
│── src
│   │── App.css
│   │── App.jsx
│   │── index.css
│   ╰── index.js
╰── src-tauri
    │── Cargo.toml
    │── build.rs
    │── icons
    │── src
    ╰── tauri.conf.json
```

#### 运行/打包项目生成客户端

修改tauri.conf配置

```json
"build": {
    "beforeBuildCommand": "npm run build",
    "beforeDevCommand": "npm run dev",
    "devPath": "http://localhost:8888",
    "distDir": "../dist",
    "withGlobalTauri": true
  },
```

```shell
npm run tauri dev
# 如果报错，试着把tauri.conf文件的tauri bundle identifier 改成 "com.tauri.build"
npm run tauri build
```

#### 安装/运行

macOS系统会自动打成dmg格式的安装包，win系统会自动打成exe安装包，双击安装运行即可。特点是**包体积小**：

[<img src="https://z1.ax1x.com/2023/11/06/piQvUrq.png" alt="piQvUrq.png" style="zoom: 50%;" />](https://imgse.com/i/piQvUrq)
