# seed-data/ — 测试基础数据使用说明

> **所属阶段**：Tasks（阶段四）
> **适用条件**：有集成测试或 E2E 测试时必需
> **更新时机**：在编写 tasks.md 前准备好

---

## 目录结构

```
seed-data/
├── README.md                    # 本文件
├── users-normal.json            # 正常用户数据
├── users-edge-cases.json        # 边界条件用户数据
├── [业务实体]-normal.json       # 正常业务数据
├── [业务实体]-edge-cases.json   # 边界条件业务数据
└── [业务实体]-errors.json       # 异常场景数据
```

## 命名规范

- 格式：`<实体名>-<场景类型>.<格式>`
- 场景类型：`normal`（正常）/ `edge-cases`（边界）/ `errors`（异常）
- 文件格式：JSON / SQL / YAML / CSV

## 数据要求

- 数据结构须与 `data-model.md` 中的表定义对齐（字段名、类型、枚举值一致）
- 数据须贴近真实业务，避免 `test123`、`foo/bar` 等无意义占位符
- 每个实体至少覆盖：正常场景、边界值、异常输入
- 敏感数据使用脱敏值（如邮箱用 `user@example.com`）
- `password` 字段存放的是 **API 请求输入**（明文），非数据库存储值；应用层负责哈希处理

---

## 示例：users-normal.json

```json
[
  {
    "email": "alice@example.com",
    "password": "SecurePass123!",
    "display_name": "Alice Wang",
    "role": "user"
  },
  {
    "email": "bob.admin@example.com",
    "password": "AdminPass456!",
    "display_name": "Bob Zhang",
    "role": "admin"
  }
]
```

## 示例：users-edge-cases.json

```json
[
  {
    "_scenario": "最短用户名",
    "email": "a@b.co",
    "password": "12345678",
    "display_name": "Li"
  },
  {
    "_scenario": "最长用户名（100字符）",
    "email": "very.long.email.address.that.reaches.the.maximum.length@example.com",
    "password": "VeryLongPasswordThatReachesTheMaximumAllowedLength123!",
    "display_name": "[100字符的显示名称]"
  },
  {
    "_scenario": "含特殊字符的用户名",
    "email": "special+chars@example.com",
    "password": "P@$$w0rd!#%",
    "display_name": "用户 (特殊字符测试)"
  }
]
```

---

## 加载方式

```bash
# 方式一：通过测试 Fixture 加载
# 在 conftest.py / setup.ts 中读取 seed-data/ 目录下的文件

# 方式二：通过脚本加载
python scripts/load_seed_data.py --dir seed-data/

# 方式三：通过 SQL 加载
psql -d [数据库名] -f seed-data/init.sql
```
