# 中国象棋 · XIANGQI

> 点击选中己方棋子，高亮显示合法着法；极小极大 AI 对弈，将军时给出警示。

用 [Zan](https://github.com/joyspinch/zan-lang) 语言写的独立游戏项目（仓库根自带 git 仓库）。完整设计与实现说明见 [`PROJECT.md`](PROJECT.md)。

## 玩法

- 点击选中己方棋子，高亮显示合法着法
- 极小极大 AI 对弈，将军时给出警示
- 将死对方主帅即获胜

## 构建

需要 [zan-lang](https://github.com/joyspinch/zan-lang) 仓库（`zanc` 编译器、公共包与 stdlib 都在里面）：

```powershell
git clone https://github.com/joyspinch/zan-lang.git
$env:ZAN_HOME = 'D:/path/to/zan-lang'   # 指到刚克隆的 zan-lang 仓库根

pwsh -File client/tools/build.ps1
```

产物：`build/xiangqi/Xiangqi.exe`（运行目录要带上它旁边的 `assets/` 与 `skins/`）。

## 运行

```powershell
cd build/xiangqi
.\Xiangqi.exe
```

## 测试

```powershell
pwsh -File client/tools/test.ps1
```

## 目录结构

```
xiangqi/
client/
  src/      # 游戏源码（.zan 源码 + HTML 界面设计稿）
  assets/   # 位图 / 音频素材
  tests/    # 玩法断言用例
  tools/    # 构建与测试脚本
PROJECT.md
```

## 素材与授权

- **大背景图已改为本地程序化生成**：`client/assets/menu_bg.png`、`menu_bg2.png`、`play_bg.png` 由仓内 `client/tools/make_bgs.py` 生成（纯 numpy + PIL，无外部素材来源），重新生成命令 `python client/tools/make_bgs.py`。
- **木纹棋盘 / 红黑棋子 / 结算面板 / 标题由图像模型生成**：这批素材源自 zan-lang 早期象棋模板，由图像模型（gpt-image-2）产出，生成管线为 zan-lang 的 `scripts/gen_assets.ps1` 与 `scripts/gen_game_art.ps1`（统一风格串见 `assets/game/style.md`，棋类品类限定词 `clean puzzle-piece iconography, flat readable shapes`），生成后做绿幕抠图与裁边缩放。逐项来源可追溯：
  - `board_wood.png` / `piece.png` —— [zan-lang `1c586f33`](https://github.com/joyspinch/zan-lang/commit/1c586f33d5f62cb835305cbbe6e2c75128b73c7e)（提交说明原文："Xiangqi: 10 endgame drills, **gpt-image** wood/piece textures"）。
  - `title.png` —— [zan-lang `50981b36`](https://github.com/joyspinch/zan-lang/commit/50981b364b3a9cfa5dac307bceb4cd702e96f916)（"Add xiangqi: alpha-beta AI, classic endgame drills, lacquer parlor art"）。
  - `board_wood2.png` / `piece_red.png` / `piece_black.png` / `panel.png` —— [zan-lang `6db0e50`](https://github.com/joyspinch/zan-lang/commit/6db0e500d8bb25c2c1547a71eb481700b67cb064)（"xiangqi: 象棋美术化——真实手绘资产接入"，手绘风格即共享风格串里的 `hand-painted digital illustration`）。
- 仓库不含任何第三方版权素材；全部位图均为本项目自产（图像模型生成或本地程序化生成）。

## 许可

本仓库采用 [MIT 许可](LICENSE)。依赖的 zan-lang 仓库采用 ZCSL（Zan Community Source License 1.0）。

## 更多文档

- [`PROJECT.md`](PROJECT.md) —— 完整设计与实现说明
- [`client/README.md`](client/README.md) —— 客户端侧说明
