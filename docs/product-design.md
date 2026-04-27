# 台球联盟管理系统 - 产品设计

## 1. 产品定位

面向台球联盟管理者，提供一站式台球厅、助教、比赛的数字化管理工具。

## 2. 用户角色

| 角色 | 权限范围 |
|------|----------|
| 联盟管理员 | 全局管理所有台球厅、助教、比赛 |
| 台球厅管理员 | 管理所属台球厅的日常运营 |

## 3. 功能模块设计

### 3.1 台球厅管理模块

**功能清单：**
- 台球厅列表（支持筛选、搜索）
- 新增/编辑/删除台球厅
- 查看台球厅详情（场地、联系人）

**数据模型：**
```
Table: billiard_clubs
- id (UUID)
- name (string)
- address (string)
- phone (string)
- business_hours (string)
- status (enum: active/inactive)
- created_at / updated_at
```

### 3.2 助教管理模块

**功能清单：**
- 助教列表（按台球厅筛选）
- 新增/编辑/删除助教
- 助教详情查看

**数据模型：**
```
Table: assistants
- id (UUID)
- name (string)
- phone (string)
- club_id (FK)
- skill_level (string)
- status (enum: employed/resigned)
- created_at / updated_at
```

### 3.3 比赛管理模块

**功能清单：**
- 比赛列表（按状态筛选）
- 创建比赛（基本信息、参赛人员）
- 比赛详情与成绩录入
- 比赛状态流转

**数据模型：**
```
Table: tournaments
- id (UUID)
- name (string)
- club_id (FK)
- start_time (datetime)
- end_time (datetime)
- format (string)  # 单败、双败、循环赛等
- status (enum: preparing/registration/open/in_progress/finished)
- created_at / updated_at

Table: tournament_participants
- id (UUID)
- tournament_id (FK)
- participant_type (enum: player/assistant)
- participant_id (FK)
```

## 4. 页面结构

```
台球联盟管理
├── 台球厅管理
│   ├── 台球厅列表
│   └── 台球厅详情/编辑
├── 助教管理
│   ├── 助教列表
│   └── 助教详情/编辑
└── 比赛管理
    ├── 比赛列表
    ├── 创建比赛
    └── 比赛详情
```

## 5. 技术选型

- **前端**：Web 应用
- **后端**：RESTful API
- **数据库**：关系型数据库

## 6. 优先级

| 阶段 | 内容 |
|------|------|
| P0 | 台球厅 CRUD、助教 CRUD |
| P1 | 比赛创建与状态管理 |
| P2 | 比赛成绩录入与展示 |
