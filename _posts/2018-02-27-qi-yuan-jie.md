---
layout: post
title: "CRM系统思考"
date: 2018-02-27
categories: 其他
---
参考 [易思普](http://www.easyserp.com/crm).

# 要开发的功能

- 客户管理
- 售后管理
- 统计报表

---

使用前后端分离技术开发。[PhalApi](https://www.phalapi.net/) 作为后端开发框架。

# 数据库开发

- 用户管理 crm_user_info
    - id
    - name
    - password
    - state
    - create_time
- 客户基本信息管理 crm_customer_info
    - id
    - name
    - phone
    - website
    - fox
    - email
    - job_super 负责人
    - phase 阶段 不确定、合同执行、合同期满、售前跟踪、售后服务
    - state 客户状态 不确定、新客户、有意向客户、潜在客户、老客户
    - business 行业 代理商、会员积分、体育健身、台球厅、快递公司、汽车美容、瑜珈馆、综合会所、美容美发、茶楼酒吧、货品提供商、高尔夫
    - type 类型 不确定、分析者、竞争者、客户、集成商、投资商、其他、合作伙伴、出版商、目标客户、经销商
    - agreement_start_date
    - agreement_end_date
    - linkman 联系人
    - versions 软件版本 普通版，白金版，辉煌版，服务器版
    - multi_version 多店版
    - dog_num 加密狗数量
    - dog_list 加密狗编号列表
    - trace_man 跟踪人员
    - bill_address 发票地址
    - bill_mail_box 发票地址邮政信箱
    - bill_city 发票地址城市
    - bill_province 发票地址省份
    - bill_postal_code 发票地址邮政编码
    - bill_country 发票地址国家
    - shipping_address 送货地址
    - shipping_mail_box 送货地址邮政信箱
    - shipping_city 送货地址城市
    - shipping_province 送货地址省份
    - shipping_mail_box 送货地址邮政编码
    - shipping_country 送货地址国家
    - memo 备注
- 维护/服务管理 crm_service_info
