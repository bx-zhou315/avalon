# Avalon

线下面对面玩《阿瓦隆》的网页助手：每人一部手机看身份、组队投票、秘密出任务牌。

- 网址：https://bx-zhou315.github.io/avalon/
- 规则：严格按官方标准规则（5–10 人，人数与任务人数按官方表格，7 人及以上第 4 个任务需 2 张失败牌，平票算否决，连续 5 次否决坏人胜，3 次成功后刺客刺杀梅林，可选湖中仙女）

## 结构

- `index.html`：整个前端（单文件，原生 JS，无构建步骤），推送到 `main` 后 GitHub Pages 自动更新
- 后端：Supabase 项目 `boardgames`（ref `usnfsfvarljsogrikcqa`，伦敦区域）
  - 表：`avalon_rooms`、`avalon_players`、`avalon_votes`、`avalon_cards`，全部开启 RLS 且没有 policy，浏览器不能直接读写
  - 所有操作都通过 `security definer` 函数（RPC），每个玩家用自己的 `token` 调用，服务器只返回该玩家应知道的信息：
    `avalon_create_room`、`avalon_join`、`avalon_remove`、`avalon_claim_seat`、`avalon_start`、`avalon_propose`、`avalon_vote`、`avalon_quest_play`、`avalon_lady`、`avalon_assassinate`、`avalon_abort`、`avalon_back_to_lobby`、`avalon_state`
  - 前端每 1.5 秒轮询 `avalon_state`
- 房间号：4 位数字；超过 2 天没动静的房间在新建房间时自动清理

## 界面

- 主题：星夜圆桌（深紫星空、金色描边），字体：霞鹜文楷（LXGW WenKai）+ Cinzel Decorative（Avalon 标志）
- 封面：湖心岛城堡 + 高背椅圆桌，角色和形象全部是代码绘制的原创 Q 版 SVG
- 玩家形象：18 个（发型 × 服饰 × 配饰组合），选中时有跳跃欢呼动画
- 测试模式：首页底部开关，可添加假玩家并切换身份，一部手机走完整局
- 房主可在游戏中「结束」本局

## 计划

- 之后加入 Secret Hitler
