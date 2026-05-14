# Sulphur-2-base Video Generation (AMD Radeon Cloud)

基于 [SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base) 的视频生成 Notebook 模板。

通过 **rclone 挂载云端硬盘**（Google Drive / OneDrive / Dropbox），实现模型和输出的持久化存储。

## 工作原理

```
首次使用：  挂载云盘 → 下载模型到云盘（一次性，~20GB）→ 生成视频
以后每次：  挂载云盘（几秒）→ 直接加载模型 → 生成视频
```

模型和生成的视频都保存在你的云盘中，实例重启不丢失。

## Model Info

| 项目 | 详情 |
|------|------|
| 模型 | SulphurAI/Sulphur-2-base |
| 架构 | DiT-based (LTX 2.3) |
| 参数量 | ~9B |
| 能力 | Text-to-Video, Image-to-Video |
| GPU | AMD Radeon (ROCm) |

## Quick Start

### 在 AMD Radeon Cloud 上使用

1. 将本仓库推到你的 GitHub
2. 在 [radeon.oneclickamd.ai](https://radeon.oneclickamd.ai/) 点击 **添加模板**
3. 资料来源填：`main/templates/Sulphur-2-base-video-generation.ipynb`
4. **发射** 实例
5. 按顺序运行 Notebook

### 首次配置云盘（只需一次，全程在 Notebook 内完成）

1. 运行 Notebook 中的"首次配置" cell
2. 它会输出一个 Google 授权链接
3. 在你的浏览器（手机/电脑都行）中打开该链接，登录并授权
4. 把得到的验证码粘贴回 Notebook
5. 运行 `!cat ~/.config/rclone/rclone.conf`，把内容保存到 Notebook 的 `RCLONE_CONFIG` 变量

**不需要在本地电脑安装任何东西。** 之后每次启动实例，Notebook 自动用保存的 token 挂载云盘。

## Structure

```
.
├── README.md
├── .gitignore
├── templates/
│   └── Sulphur-2-base-video-generation.ipynb
└── assets/
    └── .gitkeep
```

## 云盘中的目录结构

```
My Drive/
├── models/
│   └── Sulphur-2-base/     ← 模型文件（~20GB，一次性下载）
└── outputs/
    └── sulphur2/           ← 生成的视频（持久保存）
        ├── t2v_20260515_143022.mp4
        └── ...
```

## 支持的云盘

| 云盘 | rclone type | 免费空间 |
|------|-------------|----------|
| Google Drive | `drive` | 15GB（不够，需升级或用学校/公司账号） |
| OneDrive | `onedrive` | 5GB（不够，需 Microsoft 365） |
| Dropbox | `dropbox` | 2GB（不够） |
| pCloud | `pcloud` | 10GB |
| **推荐：Google Workspace** | `drive` | 学校/企业账号通常有 1TB+ |

> 注意：Sulphur-2-base 模型约 20GB，请确保你的云盘有足够空间。

## References

- [SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)
- [Lightricks/LTX-2.3](https://huggingface.co/Lightricks/LTX-2.3)
- [rclone](https://rclone.org/) — 云盘挂载工具
- [AMD Radeon Cloud](https://radeon.oneclickamd.ai/)

## License

MIT
