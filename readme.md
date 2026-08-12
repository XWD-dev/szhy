
---

# 英文外贸商城前端项目开发指令（Vue3版）

## 项目名称

**GlobalTrade-Shop**

---

## 你的角色

你是一名资深前端工程师，请帮我开发一个完整的英文版外贸电商网站用户端。

目标：

开发一个面向海外客户的 B2B 外贸独立站前端页面。

网站主要用于：

* 展示商品
* 客户浏览产品
* 加入购物车
* 提交采购询盘
* 联系供应商

不需要后台管理系统，不需要支付系统，只开发用户访问端。

---

# 一、技术要求

请使用：

* Vue3
* Vite
* JavaScript
* Vue Router
* Pinia
* Element Plus
* Axios
* CSS3

项目要求：

* 代码结构清晰
* 组件化开发
* 响应式设计
* 支持PC和手机浏览
* 所有页面英文显示
* UI风格符合欧美外贸网站习惯

---

# 二、网站整体风格

设计参考：

* Alibaba Supplier
* Shopify Independent Store
* 欧美B2B企业官网

设计要求：

* 简洁
* 商务
* 蓝白色科技风
* 大尺寸商品图片
* 突出产品展示
* 提高询盘转化

---

# 三、网站页面结构

## 1. 首页 Home

创建首页：

包含：

### 顶部导航 Header

菜单：

```
Home
Products
About Us
Contact Us
Cart
```

右侧：

* Search Products
* Shopping Cart

---

### Banner区域

包含：

大图片轮播。

文字：

```
Premium Products
Direct Factory Supply
Competitive Prices
Global Shipping
```

按钮：

```
View Products

Contact Us
```

---

### 热销产品 Featured Products

展示商品卡片：

包含：

* 商品图片
* 商品名称
* 产品价格
* MOQ
* Add To Cart按钮

---

### 公司优势 Why Choose Us

展示：

```
Factory Direct

Quality Guarantee

Global Shipping

OEM / ODM Service
```

---

### Footer

包含：

* Company Name
* Email
* WhatsApp
* Copyright

---

# 四、商品中心 Products

创建商品列表页面。

功能：

## 商品展示

每个商品显示：

* 图片
* 名称
* 价格
* 分类
* MOQ
* Add To Cart

---

## 商品搜索

支持：

关键词搜索商品。

例如：

```
Search:
LED
Speaker
Watch
```

---

## 商品筛选

支持：

Category：

```
Electronics
Lighting
Tools
Home Products
```

排序：

```
Price Low To High

Price High To Low
```

---

# 五、商品详情 Product Detail

页面包含：

## 商品图片区域

支持：

* 主图片
* 多张缩略图

---

## 产品信息

显示：

```
Product Name

Price

MOQ

Category

Supply Ability

Payment Terms
```

---

## 数量选择

功能：

```
- Quantity +
```

---

## 操作按钮

按钮：

```
Add To Cart

Send Inquiry
```

---

## 产品描述

包含：

```
Description

Specification

Packaging

Shipping Information
```

---

# 六、购物车 Shopping Cart

创建购物车页面。

功能：

商品列表：

显示：

```
Product Image

Product Name

Price

Quantity

Subtotal

Delete
```

支持：

* 增加数量
* 减少数量
* 删除商品

自动计算：

```
Subtotal

Total Amount
```

按钮：

```
Continue Shopping

Proceed Checkout
```

---

# 七、询盘订单 Checkout

外贸模式，不直接支付。

客户填写：

```
Company Name

Contact Person

Email

Phone

WhatsApp

Country

Shipping Address

Product Requirement

Message
```

按钮：

```
Submit Inquiry
```

提交后显示：

```
Thank you!
Our sales team will contact you soon.
```

---

# 八、联系我们 Contact Us

页面包含：

```
Company Information

Email

WhatsApp

Address

Contact Form
```

---

# 九、关于我们 About Us

展示：

```
Company Introduction

Factory Capability

Production Capacity

Quality Control

Global Customers
```

---

# 十、商品数据

创建模拟商品数据。

至少包含10个商品。

数据字段：

```javascript
{
id,
name,
price,
image,
category,
moq,
description,
specification
}
```

商品类别：

```
Electronics

Lighting

Tools

Home Products

Outdoor Products
```

---

# 十一、图片资源

生成：

商品图片占位方案。

目录：

```
public

/images

/banner

/products

```

要求：

每个商品都有：

* 主图
* 详情图

如果无法生成真实图片，请使用免费的图片URL。

---

# 十二、项目目录结构

生成：

```
src

├── components

│
├── views

│
├── router

│
├── store

│
├── data

│
├── assets

│
├── App.vue

└── main.js

```

---

# 十三、代码输出要求

请按照以下顺序生成：

第一阶段：

生成项目初始化配置。

包含：

* package.json
* main.js
* App.vue
* router

第二阶段：

生成公共组件：

* Header.vue
* Footer.vue
* ProductCard.vue

第三阶段：

生成页面：

* Home.vue
* Products.vue
* ProductDetail.vue
* Cart.vue
* Checkout.vue
* About.vue
* Contact.vue

第四阶段：

生成：

* Pinia购物车逻辑
* 商品数据
* CSS优化

第五阶段：

提供：

* 安装命令
* 启动命令
* 测试方法

---

# 十四、开发规则

请严格遵守：

1. 所有文字必须英文。
2. 不生成后台代码。
3. 不生成数据库。
4. 不生成登录注册。
5. 购物车使用本地状态管理。
6. 商品数据先使用Mock数据。
7. 代码必须可以直接运行。

---

# 最终目标

生成一个完整运行的：

**英文外贸商城前端网站**

用户可以：

```
访问网站

↓

浏览商品

↓

查看详情

↓

加入购物车

↓

提交采购询盘

↓

等待供应商联系
```

---

这份指令可以直接复制给AI，让它分阶段生成代码。对于你目前使用的 **VSCode + AI生成代码开发方式** 比一次性让AI生成全部代码更稳定。
