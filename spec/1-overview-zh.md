# 概述

OpenCRUD是一种完全兼容[GraphQL compliant](http://facebook.github.io/graphql/)的查询语言，用于访问和修改数据。OpenCRUD为许多流行的数据库提供API风格，包括MySQL和MongoDB。

例如，此OpenCRUD查询检索单个用户：

```graphql
{
  user(where: { id: 4 }) {
    name
  }
}
```

returns:

```json
{
  "user": {
    "name": "Mark Zuckerberg"
  }
}
```

## 依据

GraphQL是一种灵活的查询语言，支持许多不同的数据访问模式。实际上，简单的CRUD操作是一种非常常见的模式。标准化这种非常常见的模式使社区能够构建特定于常见CRUD样式API的工具。

## 参考实现

[Prisma](https://github.com/graphcool/prisma) 是OpenCRUD的参考实现
