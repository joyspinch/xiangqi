zan Xiangqi — 中国象棋（模板版）
====================================

玩法
----
- 点击选中己方棋子，高亮显示合法着法
- 极小极大 AI 对弈，将军时给出警示
- 将死对方主帅即获胜

编译
----
根目录下（公共包在 zan-lang 仓库的 packages/ 下，编译要带 --package-project）：

    pwsh -File client/tools/build.ps1

产物在 build/xiangqi/，运行所需 DLL 与 assets/ 一并落在同目录。
手动编译（同样在根目录下）：

    $env:ZAN_HOME/build/zanc.exe client/src/main.zan --auto-stdlib --package-project $env:ZAN_HOME -o build/xiangqi/Xiangqi.exe
