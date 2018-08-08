# Mutations: CRUD

* 概述
* Create
* Update
* Delete

## 概述

OpenCRUD暴露以下mutations以进行简单的数据操作

## Create

创建单个数据racord：

```graphql
mutation {
  createUser(data: { name: "Karl" }) {
    id
  }
}
```

## Update

```graphql
mutation {
  updateUser(where: { id: "1" }, data: { name: "Karl" }) {
    id
  }
}
```

## Delete

```graphql
mutation {
  deleteUser(where: { id: "1" }) {
    id
  }
}
```
