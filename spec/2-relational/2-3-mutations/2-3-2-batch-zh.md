# Mutationa: 批量操作

* 概述
* Update
* Delete

## 概述

OpenCRUD暴露了如下mutations以操纵一批数据记录。count字段返回受影响的记录数

## Update

```graphql
mutation {
  updateManyUsers(where: {name_not: "Karl"}, data:{name: "Karl"}) {
    count
  }
}
```

## Delete

```graphql
mutation {
  deleteManyUsers(where: {name_not: "Karl"}) {
    count
  }
}
```