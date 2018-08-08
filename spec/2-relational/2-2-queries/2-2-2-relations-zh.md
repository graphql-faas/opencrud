# Queries: 关系

* 概述
* 连接
  * 聚合
  * 游标
* 实例

## 概述

In relational databases a relation is used to connecto two related tables. OpenCRUD defines how relations are exposed in the GraphQL schema.
Relations in OpenCRUD generate two fields:
在关系数据库中，关联用于连接两个相关表。OpenCRUD定义了如何暴露在GraphQL schema 关联。OpenCRUD中的关联生成两个字段：

* `multi fields` 适用于需要检索相关数据的大多数情况
* `multi connection fields` 与Relay兼容并包含支持avdanced聚合的aggrete和groupBy字段。

## 连接

> WIP

## 实例

此示例说明了所有顶级字段

**数据模型**

```graphql
type User {
  id: ID! @unique
  name: String!
  posts: [Post!]!
}

type Post {
  id: ID! @unique
  title: String!
}
```

**生成的schema**

```graphql
type User implements Node {
  id: ID!
  name: String!
  posts(
    where: PostWhereInput
    orderBy: PostOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): [Post!]
  postsConnection(
    where: PostWhereInput
    orderBy: PostOrderByInput
    skip: Int
    after: String
    before: String
    first: Int
    last: Int
  ): PostConnection!
}

type Post implements Node {
  id: ID!
  title: String!
}
```

**Query**

```graphql
query {
  user(where: {id: "1"}) {
    name
    posts {
      title
    }
    postsConnection {
      edges {
        node {
          title
        }
      }
    }
  }
}
```
