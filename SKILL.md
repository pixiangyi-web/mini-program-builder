---
name: mini-program-builder
description: Use when the user wants to plan, design, prototype, build, test, or prepare a WeChat mini program or similar mobile mini app, especially one with content pages, booking flows, orders, inventory, admin management, cloud backend, launch preparation, or investor-facing demo materials. When invoked, first provide a reusable checklist of what the user should provide and what Codex will prepare, then proceed phase by phase from information architecture to UI, frontend, backend, admin, testing, and launch readiness.
metadata:
  short-description: Plan and build WeChat mini programs
---

# Mini Program Builder

Use this skill to turn a mini-program idea into a staged build plan and working artifacts. Keep it general: the business may be riding camps, lodging, courses, clinics, events, retail reservations, venues, memberships, or any appointment/order/inventory scenario.

## Default Output When Invoked

Start by giving the user an online-style fillable intake form, a fallback table, and two practical lists. The reusable intake assets live at:

- `assets/mini-program-intake-form.html` for a local browser-fillable form with export buttons
- `references/intake-table.md` for a Markdown version to copy and fill
- `assets/mini-program-intake-template.csv` for a spreadsheet version the user can fill and upload

When invoked, prefer the online-fill mode first:

- Create or copy `assets/mini-program-intake-form.html` into the project output folder.
- Tell the user to open it in the browser, fill it section by section, then export JSON or CSV.
- If the user uploads the exported JSON/CSV, parse it as the source of truth and summarize missing fields before planning.
- If the user wants to fill directly in chat, provide the Markdown table instead.

1. **可填写/上传的信息表**
   - Prefer the HTML form when the user wants an online filling experience.
   - Provide the Markdown table when the user wants to fill in chat.
   - Provide the CSV template when the user wants to fill in Excel/Numbers.
   - Tell the user that unknown fields can be filled with “待定”, and fields Codex may invent temporarily can be filled with “先用示例”.

Then give these two practical lists:

2. **需要你提供的信息**
   - 小程序名称、品牌定位、目标用户、核心转化动作
   - 业务类型：展示、预约、下单、报名、库存、会员、客服等
   - 页面范围：首页、详情页、预约页、订单页、个人中心、后台页
   - 展示资料：Logo、主图、轮播图、文案、价格、规则、地址、客服信息
   - 预约/订单规则：日期、时间段、人数、商品/服务、价格、押金/支付、取消/退款
   - 库存规则：按人、房间、设备、员工、场地、课程名额或商品库存
   - 管理需求：订单管理、库存管理、内容维护、导出 Excel、权限白名单
   - 上线资料：微信小程序账号、主体类型、域名/云开发、隐私政策、用户协议、类目、支付需求

3. **我会先准备的东西**
   - 信息架构和页面清单
   - 低保真流程图或可视化示意图
   - 高保真首页/核心页面原型
   - 可测试小程序代码
   - 模拟业务数据和库存规则
   - 云开发/后端接口方案
   - 管理端页面
   - 测试清单、上线检查清单、对外演示图或 PPT 素材

Then state a phased plan and ask only for missing high-risk inputs. If details are missing but safe to assume, use placeholder data and mark it as待替换.

## Companion Skills Used In This Workflow

When the task moves beyond planning, combine this skill with the relevant companion skills instead of treating mini-program building as a single isolated task:

- `frontend-design`: use for UI direction, homepage design, visual polish, typography, spacing, mobile layouts, and admin interface design.
- `webapp-testing`: use for local preview testing, layout checks, responsive issues, click flows, and visual regressions.
- `playwright`: use when browser automation, screenshots, form testing, or repeatable UI verification is needed.
- `browser:control-in-app-browser`: use for opening and inspecting local preview pages in the Codex in-app browser.
- `spreadsheets:Spreadsheets`: use for Excel/CSV templates, inventory exports, order exports, and structured data review.
- `documents:documents`: use for user agreements, privacy policy drafts, requirement documents, or handoff docs.
- `presentations:Presentations`: use for investor decks, product walkthrough slides, and project summary presentations.
- `imagegen`: use only when the project needs generated bitmap visuals or edited marketing-style assets; prefer user-provided real screenshots for production proof.
- `smart-explore` or `learn-codebase`: use when entering an existing codebase to understand mini-program pages, cloud functions, utilities, and data flow before editing.
- `skill-creator`: use when turning the finished workflow into a reusable skill or updating this skill.

## Phase Workflow

### 1. Clarify Business Shape

Identify the mini-program's core job:

- 内容展示：品牌、场地、服务、案例、团队、FAQ
- 交易/转化：预约、报名、下单、咨询、加微信、支付
- 运营后台：订单、库存、资料、用户、导出、通知

Decide early whether the first usable screen should be a real workflow, not a landing page. For operational tools and booking apps, prioritize direct booking entry and clear inventory/availability.

### 2. Information Architecture

Produce a concise page map:

- 用户端：首页、服务/商品列表、详情页、预约/下单页、订单页、客服/联系页
- 管理端：总览、订单列表、库存日历、内容维护、资料维护、导出
- 云端：数据表、云函数/API、权限、文件存储

For each page, define:

- 用户目的
- 必填字段
- 关键状态
- 可点击动作
- 数据来源

### 3. Data And Rules

Model the business before coding.

Common entities:

- `settings`：品牌与全局配置
- `assets`：图片、二维码、视频、文件
- `items/services`：商品、服务、课程、场地、人员或资源
- `inventory`：库存/名额/房间/设备/时段
- `orders`：订单、预约、报名
- `users/admins`：用户与管理员白名单
- `logs/notifications`：操作记录、状态变更

Common rule checks:

- 日期是否开放
- 时段是否可约
- 人数是否超过库存
- 资源是否冲突
- 房间/设备/员工/场地是否足够
- 订单状态是否允许修改
- 当前用户是否有后台权限

### 4. UI Prototype

Build a mobile-first UI. Use the brand's domain and audience to choose tone. Avoid generic template feel.

For booking mini programs:

- 首页要立刻说明业务和转化入口
- 展示内容服务于信任建立，不喧宾夺主
- 预约页要清晰显示日期、时段、余量、人数、价格/规则
- 成功页要告诉用户下一步：付款、加客服、等待确认或查看订单
- 订单页要显示状态、修改/取消规则、客服指引

Before coding, define:

- 色彩、字体、按钮、卡片、输入框、底部导航
- 图片比例和占位策略
- 空状态、加载态、错误态、无库存状态
- 小屏/大屏适配

### 5. Frontend Build

Create a testable mini-program version with placeholder data first. Keep pages scoped and easy to replace.

Recommended baseline:

- `pages/home`：首页与品牌内容
- `pages/items`：服务/商品/资源展示
- `pages/booking`：预约/报名/下单
- `pages/orders`：我的订单
- `pages/admin`：后台管理，仅管理员可见
- `utils`：日期、库存、权限、格式化
- `assets`：临时图片与品牌资源

Use real WeChat mini-program components and test in WeChat DevTools. Do not rely on browser-only behavior.

### 6. Backend And Cloud

If the user wants a working system, recommend cloud development unless they already have a server.

Typical cloud functions:

- `getConfig`
- `submitOrder`
- `getMyOrders`
- `adminListOrders`
- `adminUpdateOrder`
- `getInventoryOverview`
- `exportInventoryExcel`
- `saveContent`
- `uploadAsset`

Key backend rules:

- Never trust frontend inventory calculations alone
- Validate order creation on the cloud side
- Separate user-visible data from admin-only data
- Keep admin access controlled by whitelist/openid/role
- Log status changes

### 7. Admin Design

Make admin simple and operational, not decorative.

Useful modules:

- 今日/未来库存总览
- 订单列表与状态修改
- 内容资料维护
- 商品/服务/资源维护
- 图片上传
- Excel 导出
- 管理员白名单提示

Admin page should show only what the operator needs to act on. Use dense but readable layouts.

### 8. Testing

Test at least:

- 普通用户 vs 管理员
- 新用户首次进入
- 提交订单成功/失败
- 库存不足
- 订单重新编译后是否仍能查询
- 不同机型底部导航和按钮是否溢出
- 云函数权限和数据库权限
- 包体积、图片大小、代码质量扫描
- 微信体验版用户提交和管理员后台可见性

Use screenshots to verify layout. Fix overlapping text, cropped bottoms, too-small tap areas, and non-centered labels.

### 9. Launch Readiness

Prepare:

- 小程序名称、头像、简介、服务类目
- 主体认证：个人、个体工商户或企业
- 隐私政策、用户协议、退款/取消规则
- 云开发环境或服务器域名
- HTTPS/API 合法域名
- 微信支付商户号 if online payment is required
- 客服联系方式
- 内容版权确认
- 审核说明 and test account if needed

If the current app is under a personal主体 and later needs payment, explain that payment usually requires a suitable business主体 and merchant setup. Migration feasibility depends on whether the account/appid changes; cloud environment and openid data may need reconfiguration.

### 10. Demo And Investor Materials

When asked for presentation material:

- Use real screenshots if available
- Blur or mask names, phone numbers, order ids, QR codes, backend paths, openids, cloud env ids
- Put phone screenshot on the left and feature explanation on the right
- Keep each image self-contained
- Avoid exposing real customer data or operational credentials
- Export PNGs at a shareable resolution

## Response Style

Use practical Chinese by default when the user is Chinese. Keep outputs actionable:

- “你需要提供”
- “我会准备”
- “第一阶段/第二阶段”
- “可先用占位信息”
- “上线前必须确认”

When implementing, do not stop at planning unless the user only asks for a plan. Build, test, and report the artifact path.
