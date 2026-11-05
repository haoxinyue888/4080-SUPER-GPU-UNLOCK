<p align="center"><a href="REFERENCES.md">EN</a> | <strong>中文</strong></p>

# 研究来源与致谢

本仓库记录的是**独立的适配研究**。我们不声称发明了最初的 GPU 计算性能解锁技术，也不声称发明了基础 Windows UEFI 工作流程。

## 主要参考项目

| 项目 | 在研究传承中的作用 |
|---|---|
| [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock) | GPU 计算性能解锁的基础研究与源代码传承 |
| [JustAResearcher/gpu-unlock-ada](https://github.com/JustAResearcher/gpu-unlock-ada) | Ada 架构 GPU 解锁研究及社区成果 |
| [RTX 4080 SUPER 华硕成功报告：issue #70](https://github.com/JustAResearcher/gpu-unlock-ada/issues/70) | 独立报告的 16 GB ASUS AD103 Windows UEFI 实验。它是**另一张板卡的参考案例**，不能证明耕升显卡也兼容 |
| [TOTORONG/AD103_win_unlocker](https://huggingface.co/TOTORONG/AD103_win_unlocker) | 我们 Windows UEFI 研究的直接起点：预加载 Windows Boot Manager、人工确认、日志、图形恢复与启动交接。其原始实测对象是**改装为 32 GB 的非 SUPER 版 RTX 4080** |
| [WildFlash1st/cmp90hx-unlock](https://github.com/WildFlash1st/cmp90hx-unlock) | 更广泛的 CMP/GA102 固件研究与参考来源 |

### 其他技术背景

- [TianoCore EDK2](https://github.com/tianocore/edk2) — 研究传承中使用的 UEFI 开发接口和头文件。
- NVIDIA 的公开内核模块材料及其他固件分析工作为早期项目提供了参考；但这**不意味着**我们有权重新分发 NVIDIA 的专有固件。

## 本项目独立记录了什么

我们的新增贡献是对**一张耕升 RTX 4080 SUPER 16 GB** 的硬件特定研究：板卡与显存兼容性调查、多个 UEFI 图形子控制器的所有权验证、严格的 GOP 恢复后交接检查、不同初始状态的准入逻辑、USB 优先启动时的 Windows 查找、遇到问题即停止的日志与恢复设计、RUN00–RUN06 真实硬件观察，以及经过脱敏的 FP16/BF16 性能测试结果。

对于继承的功能——特别是原始计算解锁技术、手动按 `U` 确认和 Windows 交接概念——我们明确注明上游来源。其他显卡的成功案例**不是**本显卡兼容性的独立证明。

## 许可与发布边界

- 由 **GPL-2.0-only** 代码派生的 GPU 解锁源代码及其修改，在分发时仍须遵守适用的上游许可。本仓库仅提供研究文档，**不包含**该代码或 EFI 可执行文件。
- TOTORONG **独立撰写的说明文档**在其有权授权的范围内声明采用 **CC BY-NC 4.0**。本仓库使用自行撰写的说明，并链接原文，而非整篇复制。
- 其他上游材料可能有各自的许可要求。引用时应注明来源，不能假定一种许可证自动覆盖全部内容。
- 本仓库中**由我们独立撰写且有权授权的文字**采用 [CC BY 4.0](LICENSE)。适用范围及上游许可排除事项见[许可证范围说明](LICENSE-SCOPE.zh-CN.md)。这不会替代任何原作者另行指定的许可证。
- 不要公开私人固件文件、原始 ROM/PROM 转储、主机特定的日志、完整研究目录历史，或未经审查的可执行文件。

引用这些资料是为了**致谢、提供背景和方便进一步研究**，不表示上游作者审阅、认可或为我们的耕升实验背书。
