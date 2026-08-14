# 06 - Harbor 止损决策与封箱方案

> 决策日期：2026-08-14  
> 状态：已决定执行  
> 说明：Harbor 作为技术作品和社区贡献保留，但作为商业项目正式止损封箱。

---

## 1. 为什么止损（结论重述 & 证据）

### 1.1 跃迁目标不达标的 5 个维度

| 维度 | Harbor 现状 | 跃迁项目要求 | 差距分析 |
|---|---|---|---|
| **复利性** | ❌ 弱：一次性工具，用完即走；用户无数据沉淀；没有网络效应/UGC 飞轮 | 必须有：用得越久越离不开，内容或关系沉淀 | 插件管理本质是"设置型工具"，用户配置一次之后再也不打开；不具备复利基因 |
| **睡后收入可行性** | ❌ 几乎不可行：Godot 社区用户付费习惯极低；官方 AssetLib 是免费且有官方背书的替代品；竞品（gd-plugins 等）都停更了 | 必须有：用户有真实付费习惯，免费→付费漏斗成立 | 开发者工具 + Godot 这个定位叠加，天花板就是"卖几十份赚几百块"，ROI 不如上班 |
| **工作形态转变** | ⚠️ 间接：可以作为作品集证明工程能力，但路径非常长 | 最好直接：产品上线直接带来收入，不依赖面试/接单 | Harbor 带来的作品集价值可被其他项目替代（比如这个拼豆工具，技术栈展示效果甚至更好） |
| **天花板** | ❌ 低：目标用户 = Godot 开发者（全球百万级，但国内极少）；付费转化率 < 1%；月收入天花板百级到千级人民币 | 必须高：市场量级千万+，或横向扩展路径清晰 | 不做横向扩展就是死；但横向扩展到 Unity/Unreal 插件管理的话维护量 ×3，且 Unity Store 已有成熟方案 |
| **维护负担** | ⚠️ 高：Tauri 桌面端 × Rust 后端 × Vue 前端 × 5 个模板仓库 × Apple/Windows 签名分发 × Godot 生态跟踪（每个大版本插件都可能失效） | 必须低：MVP 阶段单人能 handle，维护小时数/月 < 10 | 每月维护 20+ 小时，换来收益接近于 0，时薪 < 一杯奶茶钱 |

### 1.2 反事实推演：如果不停 Harbor，1 年后会怎样？

推演剧本（不封箱的最可能结局）：
1. 花 2 个月补完签名分发 + 上架模板到 AssetLib
2. 获得 100-200 个下载用户，10 人 Star
3. 每月花 10-20 小时修兼容 + 回 issue
4. 一年后：500 用户 / 0 付费 / 维护累计 200 小时 / 个人作品集增加 1 个
5. 然后因为 Godot 5.0 API 大改又要重做一轮，崩溃放弃

同样 200 小时投入拼豆纠错工具，最保守算：
- 3000 用户 / 150 付费 / 月收入 ¥1500 / 有复利 / 可横向扩展
- 作品集展示效果：移动端 + CV + 商业闭环 >> 纯桌面插件管理

---

## 2. 封箱方案（不是删除，是"存档保留"）

### 2.1 封箱原则

1. **不删代码**：所有仓库 public 保留，README 第一行加状态徽章「Status: Archived (Sealed)」
2. **不删 Issue/PR**：社区历史保留
3. **不做新功能**：任何 Feature Request 统一回复「此项目已封箱，不再接受新功能 PR」
4. **最低兼容维护**：Godot 大版本（如 4.5/5.0）发布后，花 2-4 小时修核心崩溃和编译错误，保证不彻底挂掉
5. **不投钱**：Apple 开发者证书如果过期且 Harbor 是唯一用途，就不续费；模板上架 AssetLib 动作取消

### 2.2 各仓库封箱动作清单

| 仓库 | 当前状态 | 封箱动作 | 截止日期 |
|---|---|---|---|
| **GodotHarbor 主仓**（本仓） | Tauri + Rust + Vue 前端 + 原内置模板 | ① README 顶部加「Sealed」徽章 + 一段话解释封箱原因和后续方向 ② 开 issue 置顶说明封箱 ③ 关闭 Project Board 的所有 To-do ④ tag `v0.1.0-sealed` | 2026-08-31 |
| **harbor-bootstrap**（独立仓） | EditorPlugin 引导脚本 | ① 同样加 Sealed 徽章 ② 说明：此插件可继续作为 Godot 模板里引导用户使用自定义 App 的范例 ③ tag `v1.0.0-sealed` | 2026-08-31 |
| **godot-template-2d-platformer** | 模板独立仓 | ① 保留且 **继续维护**：即使没有 Harbor，模板本身是好的作品集，可上传 AssetLib / itch.io 获得 Star ② README 更新：去除"推荐使用 Harbor"的引导，改为模板本身的介绍 ③ 如用户问"Harbor 是什么"，统一回"Harbor 已停止开发，模板可直接独立使用" | 2026-09-15 |
| **godot-template-2d-rpg** | 模板独立仓 | 同上：保留+继续维护（独立价值），去 Harbor 引导 | 2026-09-15 |
| **godot-template-3d-starter** | 模板独立仓 | 同上：保留+继续维护，去 Harbor 引导 | 2026-09-15 |
| **godot-template-multiplayer** | 模板独立仓 | 同上：保留+继续维护，去 Harbor 引导 | 2026-09-15 |
| **godot-template-starter-framework** | 新建的独立框架（主菜单/暂停/存档等） | **重点保留并独立发展**：这个模板本身社区价值很高（主菜单/暂停/存档/选项/ Credits 通用框架），可以持续迭代功能做成 Godot 版的"Unity Starter Assets"，独立拉 Star 和社区口碑 | 长期维护 |

### 2.3 README 封箱徽章与文案参考

```markdown
<!-- 放在 GodotHarbor 主仓 README 最顶部 -->

<div align="center">

# ⚓ GodotHarbor

[![Status: Sealed](https://img.shields.io/badge/Status-Sealed-blueviolet)](https://github.com/yourname/bead-ai-corrector-planning)
[![Godot 4.3+](https://img.shields.io/badge/Godot-4.3%2B-blue)](https://godotengine.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Status Update (2026-08): This project is sealed.**  
No new features will be developed. Critical compatibility fixes will be provided on a best-effort basis for major Godot releases.

→ **I'm now working on a new indie project:** [拼豆 AI 纠错工具](https://github.com/yourname/bead-ai-corrector-planning) — an AI-powered physical error correction tool for Perler Beads / Cross Stitch / Diamond Painting hobbyists.

</div>

---

（原 README 内容保留，不删）
```

---

## 3. 资产处置与迁移

### 3.1 可复用资产 → 迁移到新项目

| Harbor 的资产 | 是否可复用 | 复用到拼豆项目的哪里 | 说明 |
|---|---|---|---|
| **Tauri + Rust 工程实践** | ✅ 间接 | 新项目用 Flutter，不直接复用；但 Rust 写 CV 绑定（flutter_rust_bridge）的经验可迁移 | 不是代码复用，是经验复用 |
| **Vue 前端组件设计** | ⚠️ 有限 | 状态机思路、用户流程设计可参考；UI 组件不直接搬 | Flutter 组件体系完全不同 |
| **harbor-bootstrap 的"首次启动引导 + 不再提示模式"** | ✅ 高度复用 | 拼豆 App 的首次冷启动 30 秒引导 + 每日免费次数用完提醒 | 交互逻辑和状态机（dismissed / installed / triggered 等）直接抄 |
| **harbor lock 的 Hash 校验思路** | ❌ 不相关 | - | 新项目不需要 |
| **模板项目独立仓库拆分 + 同步脚本经验** | ⚠️ 间接 | Stage 3 扩展十字绣/钻石画品类时，多品类管理思路可以参考 | 管理经验复用 |
| **独立开发者身份 / GitHub 作品集展示** | ✅ 直接 | 新项目 README 可以写「Author of GodotHarbor (xxx Stars)」增加可信度 | 身份背书复用 |
| **Godot 社区人脉 / Discord 服务器** | ⚠️ 有限 | 拼豆用户和 Godot 用户不重叠；但可以在朋友圈/技术群宣传新项目时触达同好 | 小范围渠道复用 |

### 3.2 不再需要的资产（保留但不维护）

- Apple Developer 签名证书 / 公证脚本：如果拼豆项目（iOS App）用到就续，不用就过期（反正 ¥688/年，看新项目决定）
- sync-templates.ps1 等 Harbor 专属脚本：保留在仓里但标记 deprecated
- harbor:// deep link 协议、takeover_project 命令、harbor-bridge 插件注入逻辑：全部废弃，不再维护

---

## 4. 封箱的心理建设（为什么不是"失败"）

> 这是决策日志，写给几个月后可能后悔的自己看。

1. **及时止损不是失败，继续投入才是**。花了很多时间做 Harbor ≠ 必须继续做下去（沉没成本谬误）。
2. **Harbor 的价值不是零**：它让你完整跑通了"一个桌面工具从 0 到可发布"的全流程（Tauri/Rust/前端/签名/插件机制/模板生态），这些经验 100% 复用到新项目。
3. **作品集视角**：GitHub 上保留 1 个封箱但技术完整的 Godot 插件管理器 + 5 个可运行的游戏模板，比 1 个半死不活更有展示效果。
4. **跃迁视角**：把 Harbor 投入的时间看作"跃迁项目的学费"，不算亏。真正亏的是知道不行还死磕一年。
5. **回退方案保留**：如果 3 个月后拼豆项目验证完全失败，可以随时回来解封 Harbor（代码都在），只是换方向的代价极低。

---

## 5. 封箱执行 Checklist

- [ ] GodotHarbor 主仓 README 加 Sealed 徽章 + 状态文案 + 指拼豆项目链接
- [ ] 主仓开置顶 Issue 说明封箱决策和原因
- [ ] 主仓打 tag `v0.1.0-sealed`
- [ ] harbor-bootstrap 仓同样加 Sealed 徽章 + tag
- [ ] 4 个模板仓库 README 去除"推荐使用 Harbor"引导，强调可独立使用
- [ ] starter-framework 模板 README 更新为独立定位（不依赖 Harbor）
- [ ] 所有仓库 Project Board 的 To-do 全部 Close，并加「封箱不再推进」标签
- [ ] 本地 Harbor 开发相关分支整理（未合并的 feature/ 分支删掉或归档）
- [ ] 写一篇个人朋友圈/即刻长文：「为什么我放弃了做了半年的 Godot 插件管理器，转向拼豆 AI 纠错？」（可选，看个人偏好）
