## SakuraLLMServer
- 运行 [SakuraLLM](https://github.com/SakuraLLM/SakuraLLM) 轻小说翻译模型的服务器端一键包
- 提供的配置按照与 [AiNiee](https://github.com/NEKOparapa/AiNiee) 翻译器搭配使用设计，其他用途是否合适请自行判断

## 要求
- 至少 8G 显存 Nvidia 独立显卡
- 确保安装了最新版本的显卡驱动程序

## 步骤
- 从 [发布页](https://github.com/neavo/SakuraLLMServer/releases) 下载最新版本的 `SakuraLLMServer` 并解压缩
- 根据显存大小下载适合的模型并放入 `SakuraLLMServer` 文件夹。

| 显存大小         | 模型规模     | 下载链接                                                  |
|:---------------:|:-----------:|:---------------------------------------------------------:|
| 8G              | 7B          | [Galtransl-7B-v2-IQ4_XS.gguf](https://huggingface.co/SakuraLLM/GalTransl-7B-v2/blob/main/Galtransl-7B-v2-IQ4_XS.gguf) |
| 8G              | 14B         | [sakura0.92_1.11_IQ3XSS.gguf](https://huggingface.co/shing3232/sakura-14b-qwen2beta-v0.9.2-IMX/blob/main/sakura0.92_1.11_IQ3XSS.gguf) |
| 10G             | 14B         | [sakura0.92_1.11_IQ3XSS.gguf](https://huggingface.co/shing3232/sakura-14b-qwen2beta-v0.9.2-IMX/blob/main/sakura0.92_1.11_IQ3XSS.gguf) |
| 11G/12G/16G/24G | 14B         | [sakura-14b-qwen2beta-v0.9.2-iq4xs.gguf](https://huggingface.co/SakuraLLM/Sakura-14B-Qwen2beta-v0.9.2-GGUF/blob/main/sakura-14b-qwen2beta-v0.9.2-iq4xs.gguf) |

## 启动
- 现在你的文件结构应该类似于：
```
  SakuraLLMServer\llama\...
                    \00_Core.bat
                    \01_768_NP4_KVQ4.bat
                    \Galtransl-7B-v2-IQ4_XS.gguf
                    \...
```
- 根据 `你的显存和模型的搭配组合` 选择对应的启动脚本，双击启动即可
  
| 显存大小         | 模型规模     | 启动脚本             |
|:---------------:|:-----------:|:--------------------:|
| 8G              | 7B          | 01_800_NP8_KVQ4.bat  |
| 8G              | 14B         | 01_768_NP4_KVQ4.bat  |
| 10G             | 14B         | 01_800_NP8_KVQ4.bat  |
| 11G/12G/16G/24G | 14B         | 01_800_NP16_KVQ4.bat |
| 24G             | 14B         | 01_800_NP32_KVQ4.bat |

## 设置 AiNiee 
- 确保启动 [AiNiee](https://github.com/NEKOparapa/AiNiee) 应用，并根据 `显存大小` 设置以下选项：
  
| 选项 | 设置 |
|------|:----:|
| 翻译设置 - 发送设置 - 使用 Tokens 模式      | 启用                      |
| 翻译设置 - 发送设置 - 每次翻译 Tokens       | 384                       |
| 翻译设置 - 发送设置 - 最大线程数            | 启动脚本名称中 NP 后的数字  |
| 翻译设置 - 发送设置 - 错误重翻最大次数限制   | 1                         |
| 翻译设置 - 发送设置 - 翻译流程最大轮次限制   | 10                        |
| 翻译设置 - 专项设置 - 执行替换后翻译         | 启用                      |
| 翻译设置 - 专项设置 - 处理首尾非字符文本     | 启用                       |

## 其他说明
- 为何 `8G` 显存有两种配置
  - `14B` 模型的翻译能力显著强于 `7B` 模型，但是 `8G` 显存运行 `14B` 模型有些紧张
  - 使用 `8G+14B` 配置时，应尽量关闭 `VSCode`、`浏览器`、`动态壁纸`、`视频播放器` 等应用以释放显存
  - 如果还是会 `爆显存`，则考虑降级至 `8G+7B` 配置
  - 其他配置组合显存都比较宽裕，一般不会 `爆显存`
- 如何判断是否 `爆显存`
  - 如果爆的比较厉害，程序会直接报错或者退出
  - 爆了一点又没有完全爆比较难判断
  - 一个可参考的方式是通过第三方软件监测显卡功耗
  - 满载执行任务时，显卡实际功耗应为最大功耗的 `70%-80%`，如果很低则大概率是爆显存了

