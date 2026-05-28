---
type: source
title: "bash read 会吃掉前导空格"
slug: bash-read-ifs-space-trimming
status: insight
created: 2026-05-28
updated: 2026-05-28
category: devops
---
# bash read 会吃掉前导空格
bash `read` 默认以 `$IFS`（空格、制表符、换行）为分隔符，会吃掉输入的前导空格。输入"空格+回车"后变量值为空字符串，不是空格。

**解决**：用 `IFS= read -r confirm` 保留原始输入。

确认脚本模式（回车确认、空格取消）：
```bash
IFS= read -r confirm
if [[ "$confirm" == " " ]]; then
  echo "已取消"
else
  # 直接回车 → $confirm 为空 → 执行
  herdr pane close "$pane_id"
fi
```

关键点：
- `IFS=` 防止空格被截断
- `-r` 防止反斜杠转义
- `[[ "$confirm" == " " ]]` 精确匹配单个空格
*Category: devops*
---
*Captured: 2026-05-28*
## Related
_Add links to related pages._