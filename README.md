# mini-program-builder

一个用于从 0 到 1 规划、设计、搭建、测试并准备上线微信小程序的 Codex skill。

它适合预约、报名、订单、库存、内容展示、后台管理、云开发、Excel 导出、上线准备、投资人/面试展示等常见小程序项目。

## What It Does

调用这个 skill 后，Codex 会先帮你整理：

- 你需要提供哪些资料
- 哪些信息可以先用示例占位
- 小程序应该有哪些页面
- 预约、订单、库存、后台和上线规则怎么拆
- Codex 可以先准备哪些原型、代码、表格、测试清单和展示材料

然后按阶段推进：

1. 业务和目标用户梳理
2. 页面结构和信息架构
3. 数据表、库存和订单规则
4. 移动端 UI 原型
5. 微信小程序前端
6. 云开发/后端接口
7. 后台管理
8. 测试和上线检查
9. 对外演示图、文档或 PPT

## Included Templates

这个 skill 自带三种资料收集模板：

- `assets/mini-program-intake-form.html`：可在浏览器填写的在线表单，可导出 JSON/CSV
- `assets/mini-program-intake-template.csv`：可用 Excel/Numbers 填写的表格
- `references/intake-table.md`：可直接复制到聊天里填写的 Markdown 表

不知道的信息可以写“待定”，想先推进的内容可以写“先用示例”。

## When To Use

适合这些请求：

- “我想做一个微信小程序，帮我规划”
- “帮我搭一个可测试的小程序版本”
- “帮我做预约/订单/库存/后台”
- “帮我准备小程序上线清单”
- “帮我把这个小程序整理成融资/面试展示材料”
- “先给我一份需要填写和上传的信息表”

## Install

把整个文件夹放到你的 Codex skills 目录：

```text
~/.codex/skills/mini-program-builder
```

目录结构应类似：

```text
mini-program-builder/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
├── assets/
│   ├── mini-program-intake-form.html
│   └── mini-program-intake-template.csv
└── references/
    └── intake-table.md
```

## Example Prompt

```text
使用 mini-program-builder，帮我规划并搭建一个预约类微信小程序。
先给我可填写的信息表，缺失内容先用示例数据推进。
```

## Notes

- 这个 skill 不绑定具体行业，可用于营地、课程、门店、场馆、医疗、活动、零售预约等项目。
- 如果项目需要视觉设计、测试、Excel、文档或演示材料，它会提示搭配对应的 companion skills。
- 如果后续需要微信支付，主体认证、商户号、云环境和数据迁移需要单独确认。
