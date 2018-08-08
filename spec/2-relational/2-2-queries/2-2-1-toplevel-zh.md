# Queries: 顶级

* 概述
* 单字段多字段
* 多连接字段
* 节点字段
* 例子

## 概述

GraphQL定义顶级`Query`类型。OpenCRUD定义了为每种数据库类型生成的多个顶级字段（关系数据库中的表）
s

## 单字段

检索单个数据记录。

## 多字段

检索多个数据记录

## 多连接字段

检索多个数据记录。此字段兼容[Relay compliant](https://facebook.github.io/relay/docs/en/graphql-server-specification.html)，同时包含子字段`aggregate`和`groupBy`子字段。


## 节点字段

节点字段由[Relay spec](https://facebook.github.io/relay/docs/en/graphql-server-specification.html)规范指定，并允许客户端通过其id检索任何数据记录。

## 命名

OpenCRUD未指定必须如何命名为每种数据类型生成的字段。由每个OpenCRUD实现决定一个命名系统。参考实现使用followig命名约定：

- 单字段： `[data type name]`
- 多字段: `[pluralized data type name]` (using the [evo-inflector library](https://github.com/atteo/evo-inflector))
- 多连接字段：`[pluralized data type name]Connection`

OpenCRUD实现可以选择使字段名称可配置而不是基于约定。


## 示例

此示例说明了所有顶级字段

**数据模型**

```graphql
type User {
  id: ID! @unique
  name: String!
}
```

**生成的schema**

```graphql
type Query {
  users(
    where: UserWhereInput
    orderBy: UserOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): [User]!
  user(where: UserWhereUniqueInput!): User
  usersConnection(
    where: UserWhereInput
    orderBy: UserOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): UserConnection!
  node(id: ID!): Node
}
```

**Query**

```graphql
query {
  user(where: { id: "1" }) {
    name
  }
  users(where: { name_contains: "Karl" }) {
    name
  }
  usersConnection(where: { name_contains: "Karl" }) {
    edges {
      node {
        name
      }
    }
  }
  node(id: "1") {
    name
  }
}
```
