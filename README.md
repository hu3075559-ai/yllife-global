# yllife-global

源莱生活 · 海外版（阶段 0 需求验证），静态单页，Cloudflare Pages 托管：
https://yllife-global.pages.dev

面向海外华人：把 Labcorp / Quest 的英文体检报告解读成中文
（逐项人话解释、单位双显、附可转发给医生的英文摘要）。
定位口径（硬）：健康信息解读，**不替代医生诊断**。

## 阶段 0 验证页结构

- `/` 单页：痛点首屏＋示例解读样张（虚构人物"陈女士 58 岁"，
  Labcorp 风格摘录 12 项、3 项异常，全区显著标注"示例·虚构数据"）
  ＋怎么运作（人工＋AI 辅助、24–48h 交付）＋隐私承诺＋$5 早鸟预订
  ＋双表单（免费试单 / 等候名单）＋FAQ。
- 双表单走 leads-api（POST https://lunasign.me/api/leads，
  site=yllife-global；source=trial / waitlist 分流；渠道归因读
  URL 的 ?src= 参数写入 note，无参数记 direct）。
- $5 预订按钮当前为**意向登记**：收款账户（Stripe）待用户确定后，
  把链接填进 index.html 脚本顶部的 PREORDER_PAYMENT_URL 常量并改
  按钮行为；在此之前不产生任何收费。
- **隐私强制项（方案定版）**：页面不装任何广告追踪像素与分析脚本
  （无 GA、无 51.la、无 Meta Pixel），统计只靠 leads 的 src 标记。

## Layout / publishing

只有 `public/` 发布：Pages 项目 destination_dir=public。内容正本即
`public/index.html`（单文件含样式与脚本），改完经 gh.py 推送，
Pages 自动部署。

## 判定线（阶段 0，2 周）

等候名单 ≥200 或付费预订意向 ≥20 或试单 ≥15 单，任一达标 → 进开发；
全不达标 → 停。
