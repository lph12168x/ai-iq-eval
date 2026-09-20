# AI IQ Eval

用同一道"动画 SVG"题目横向评测不同大模型 × 编码 Agent 组合的图形建模与动画工程能力。

## 评测题目

每道题目独立成一个目录，产物放在各自目录内；当前收录 `pelican_bicycle/`。

生成一只**鹈鹕骑自行车**的动画 SVG：要求自行车有车轮转动、曲柄踏板联动，鹈鹕有蹬腿动作。

题目看似简单，实则同时考察：

- **几何与结构**：车架菱形、轮径、曲柄半径、链条与踏板的相对位置是否自洽
- **运动学**：腿部双段骨骼的 IK 解算，脚掌是否始终贴合踏板而不脱节
- **渲染器兼容性**：`transform-origin` / `transform-box` 在 CSS 与 SMIL 混用时的差异
- **代码组织**：动画分层（位移走 CSS、旋转形变走 SMIL）与可读性

## 命名规范

```
<provider>_<model>_<variant>_<agent>.svg
```

| 字段 | 含义 | 观测取值 |
| --- | --- | --- |
| `provider` | 模型供应商 | `cmdcode` `traecode` `nous` `openrouter` `opencode` |
| `model` | 模型名，内部以 `-` 分隔 | `deepseek-v4.1-flash` `glm-5.3-flash` `gpt-5.6-luna` `qwen-3.8-flash` `mimo-v2.6-flash` `kimi-k2.8-preview` `seed-2.1-pro-0915` `seed-code` `union-alpha` |
| `variant` | 推理强度，后续会测其他档位 | `high`（当前全部） |
| `agent` | 产出该 SVG 的编码 Agent | `pi` `zcode` `traecode` `opencode` |

示例：`cmdcode_glm-5.3-flash_high_pi.svg` → `provider=cmdcode`、`model=glm-5.3-flash`、`variant=high`、`agent=pi`。

## 样本清单

| 供应商 | 模型 | 推理强度 | Agent | 产物 | 体积 |
| --- | --- | --- | --- | --- | --- |
| `cmdcode` | `deepseek-v4.1-flash` | `high` | `zcode` | [svg](pelican_bicycle/cmdcode_deepseek-v4.1-flash_high_zcode.svg) | 20.0 KB |
| `cmdcode` | `glm-5.3-flash` | `high` | `pi` | [svg](pelican_bicycle/cmdcode_glm-5.3-flash_high_pi.svg) | 8.1 KB |
| `cmdcode` | `glm-5.3-flash` | `high` | `zcode` | [svg](pelican_bicycle/cmdcode_glm-5.3-flash_high_zcode.svg) | 9.8 KB |
| `cmdcode` | `gpt-5.6-luna` | `high` | `pi` | [svg](pelican_bicycle/cmdcode_gpt-5.6-luna_high_pi.svg) | 12.3 KB |
| `cmdcode` | `qwen-3.8-flash` | `high` | `pi` | [svg](pelican_bicycle/cmdcode_qwen-3.8-flash_high_pi.svg) | 25.7 KB |
| `nous` | `gpt-5.6-luna` | `high` | `pi` | [svg](pelican_bicycle/nous_gpt-5.6-luna_high_pi.svg) | 8.2 KB |
| `opencode` | `mimo-v2.6-flash` | `high` | `opencode` | [svg](pelican_bicycle/opencode_mimo-v2.6-flash_high_opencode.svg) | 19.8 KB |
| `openrouter` | `union-alpha` | `high` | `pi` | [svg](pelican_bicycle/openrouter_union-alpha_high_pi.svg) | 6.0 KB |
| `traecode` | `kimi-k2.8-preview` | `high` | `traecode` | [svg](pelican_bicycle/traecode_kimi-k2.8-preview_high_traecode.svg) | 13.3 KB |
| `traecode` | `seed-2.1-pro-0915` | `high` | `traecode` | [svg](pelican_bicycle/traecode_seed-2.1-pro-0915_high_traecode.svg) | 22.6 KB |
| `traecode` | `seed-code` | `high` | `traecode` | [svg](pelican_bicycle/traecode_seed-code_high_traecode.svg) | 10.4 KB |

同一模型经不同供应商/Agent 产出的结果差异，也是本仓库关注的对比维度（如 `glm-5.3-flash` 的 `pi` / `zcode` 两份，`gpt-5.6-luna` 的 `cmdcode` / `nous` 两份）。

## 预览

![pelican riding a bicycle](pelican_bicycle/cmdcode_deepseek-v4.1-flash_high_zcode.svg)

## 本地查看

产物均为自包含 SVG，不含外部依赖与脚本，直接用浏览器打开即可播放动画：

```shell
xdg-open pelican_bicycle/cmdcode_deepseek-v4.1-flash_high_zcode.svg
```

## 许可

AGPL-3.0，详见 [LICENSE](LICENSE)。
