# Auto Accept Agent

[English](README_EN.md) | **中文**

一个 VS Code / Antigravity / Cursor 扩展，自动接受 AI 代理的操作请求，省去频繁的手动审批。

---

## 功能

- 自动接受文件编辑、终端命令、重试提示等 14 种操作类型
- 设置面板可勾选需要自动接受的操作类型
- 后台模式，同时管理多个对话标签页
- 内置危险命令拦截（如 `rm -rf /`）
- 状态栏实时显示运行状态
- 自动检测 CDP 调试端口
- 支持英文和简体中文

## 安装

1. 下载 `.vsix` 文件
2. 打开 IDE，按 `Ctrl+Shift+P`，输入 `Install from VSIX`
3. 选择文件，重启 IDE

## 使用

点击状态栏的 `Auto Accept: OFF` 即可开启。首次使用需要允许快捷方式更新（添加 `--remote-debugging-port=9000` 参数），之后自动运行。

## 配置

| 配置 | 说明 | 默认值 |
|------|------|--------|
| CDP 端口 | 调试协议端口号 | 自动检测 |
| 自动接受文件编辑 | 是否自动应用文件更改 | 开启 |
| 语言覆盖 | 强制指定界面语言 | 自动 |
| Overlay 模式 | 后台模式显示方式 | 关闭 |
| 操作类型选择 | 选择需要自动接受的操作 | 仅 run |

## 兼容性

支持 VS Code / Antigravity / Cursor，Windows / macOS / Linux，多窗口多实例，最小化和失焦状态下均可正常工作。

## 许可证

[MIT](LICENSE.md)