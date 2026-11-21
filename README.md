# Smart JSON Parser

一个可以离线使用的单文件 JSON 解析工具。直接用浏览器打开 `smart-json-parser.html` 即可使用，无需安装依赖或启动服务器。解析在浏览器内完成，输入内容不会上传。

## 快速开始

1. 下载 [smart-json-parser.html](./smart-json-parser.html)，用现代浏览器打开。
2. 在左侧粘贴文本，工具会自动解析。也可以点击「解析」，或按 `Ctrl / ⌘ + Enter`。
3. 在右侧查看解析路径、切换候选，并搜索键或值。点击「载入示例」可体验日志提取和嵌套展开。

## 支持的输入

| 格式 | 示例 |
| --- | --- |
| 标准 JSON | `{"a":1,"b":[true,null]}` |
| 宽松 JSON | `{name: 'Ada', ready: True, parent: None,}`。支持注释、尾逗号、单引号和未加引号的键。 |
| 多层转义 | `{\"a\":1}`，也可识别多层引号包装。 |
| 日志中的 JSON | `INFO checkout {"id":1,"message":"括号 } 也是文本"} done` |
| 查询串与完整 URL | `a=1&name=Ada+Lovelace` 或 `https://example.com/?tag=one&tag=two`。自动解码参数，重复的键保留为数组。 |
| URL 编码与 Base64 | `%7B%22a%22%3A1%7D` 或 `eyJhIjoxfQ==` |
| Java Map | `{name=Ada, active=true, items=[1, 2]}` |
| 多段 JSON | `{"a":1} {"b":2}`，合并为数组。也支持每行一段的 NDJSON。 |

## 查看与导出

- 解析器用有界的广度优先搜索尝试反转义、URL 解码、Base64 解码和片段提取等操作。优先展示对象或数组，再按叶子数从多到少、解析步骤从少到多排序。
- 自动检查字符串字段中可继续解析的 JSON 和查询串，并用徽标标记展开的位置。顶部显示顶层字段、叶子节点、嵌套展开和输入长度。
- 支持筛选高亮、展开和折叠结果树、复制和下载 JSON。开启压缩视图时，复制和下载会输出紧凑 JSON。
- 支持中英文和深浅主题。解析在 Web Worker 中执行，超时默认 3 秒，可调至 2–6 秒。单次输入上限为 100 万字符。
