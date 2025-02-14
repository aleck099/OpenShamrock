---
title: 消息格式
icon: message
---

::: tip 提示
在后续的文档中，我们将提供 CQ 码和消息段两种格式的消息示例，以便于您更好地理解。
:::

## CQ 码

CQ 码是一种特殊的文本格式，用于在消息中插入表情、图片、音乐、语音、视频、网页等内容。

### 格式

这是一个 CQ 码的基本格式：

```text
[CQ:action,param1=value1,param2=value2]
```

CQ 码中内容含义如下：

- `action`：动作，指示要进行的操作，如发送图片、音乐等。
- `param`：对应动作需要的参数，如 `qq`、`file` 等。
- `value`：参数所对应的值，如 AT 的 QQ 号。

### 示例

例如，要 AT 一个 QQ 号为 `123456` 的用户，可以这样写：

```text
[CQ:at,qq=123456] Hello!
```

他会被解析为：

```text
@小明 Hello!
```

### 转义

CQ 码由 `[` 和 `]` 并以 `,` 分隔的多个部分组成，因此如果要在 CQ 码中使用这些字符，需要进行转义。

| 原字符 | 转义字符 |
| ------ | -------- |
| `&`    | `&amp;`  |
| `[`    | `&#91;`  |
| `]`    | `&#93;`  |
| `,`    | `&#44;`  |

## 消息段

消息段是新一代的消息格式，采用 JSON 格式。

### 格式

消息段是一个 JSON 对象，以下是一个消息段的基本格式：

```json
{
  "type": "text", // 消息段类型
  "data": {
    // 消息段数据/参数
    "text": "Hello!"
  }
}
```

### 示例

例如，要 AT 一个 QQ 号为 `123456` 的用户，可以这样写：

```json
{
  "type": "at",
  "data": {
    "qq": 123456
  }
}
```

他会被解析为：

```text
@小明
```

### 组合

消息段可以组合在一起，形成一个消息。

```json
[
  {
    "type": "at",
    "data": {
      "qq": 123456
    }
  },
  {
    "type": "text",
    "data": {
      "text": " Hello!"
    }
  }
]
```

以上消息段会被解析为：

```text
@小明 Hello!
```
