# Queries: 过滤器

* 概述
* 数据类型
* 单字段
* 多字段
* 布尔表达式
* 交叉关系过滤器

## 概述

OpenCRUD过滤器旨在尽可能多地显示底层数据库的功能，同时保持简单直观的API接口。过滤器可用于所有顶级字段和关系字段。

## 数据类型


可用的过滤器取决于字段的类型。例如，Integer字段支持大于过滤器，而String字段支持在子字符串上匹配的contains过滤器。

```graphql
type UserWhereInput {
  AND: [UserWhereInput]
  OR: [UserWhereInput]

  # String field
  field: String # equals
  field_not: String # not equals
  field_contains: String # contains substring
  field_not_contains: String # does not contain substring
  field_starts_with: String
  field_not_starts_with: String
  field_ends_with: String
  field_not_ends_with: String
  field_lt: String # less than
  field_lte: String # less then or equals
  field_gt: String # greater than
  field_gte: String # greater than or equals
  field_in: [String] # in list
  field_not_in: [String] # not in list

  # Integer field
  field: Integer # equals
  field_not: Integer # not equals
  field_lt: Integer # less than
  field_lte: Integer # less then or equals
  field_gt: Integer # greater than
  field_gte: Integer # greater than or equals
  field_in: [Integer] # in list
  field_not_in: [Integer] # not in list
  
  # Float field
  field: Float # equals
  field_not: Float # not equals
  field_lt: Float # less than
  field_lte: Float # less then or equals
  field_gt: Float # greater than
  field_gte: Float # greater than or equals
  field_in: [Float] # in list
  field_not_in: [Float] # not in list
  
  # Boolean field
  field: Boolean # equals
  field_not: Boolean # not equals
  
  # DateTime field
  field: DateTime # equals
  field_not: DateTime # not equals
  field_in: [DateTime] # in list
  field_not_in: [DateTime] # not in list
  field_lt: DateTime # less than
  field_lte: DateTime # less then or equals
  field_gt: DateTime # greater than
  field_gte: DateTime # greater than or equals
  
  # Enum field
  field: Enum # equals
  field_not: Enum # not equals
  field_in: [Enum] # in list
  field_not_in: [Enum] # not in list
  
  # List[T] field
  field_contains: T # contains single scalar T
  field_contains_every: [T] # contains all scalar T
  field_contains_some: [T] # contains at least 1 scalar T
 
  # many Relation field
   field_every: FilterCondition # condition must be true for all nodes
  field_some: FilterCondition # condition must be true for at least 1 node
  field_none: FilterCondition # condition must be false for all nodes
  field_is_null: Boolean # is the relation field null
 
  # one Relation field
  field: UserWhereInput # condition must be true for related node
}
```

## 单字段

与单个数据记录关系的字段允许您按唯一字段上的完全匹配进行过滤：

```graphql
{
  user(where: {id: "1"}){
    name
  }
}
```

## 多字段

与许多数据记录关系的字段允许按上面指定的所有过滤器进行过滤：

```graphql
{
  users(where: {name_not_in:["Karl", "Viggo"]}){
    name
  }
}
```

## 布尔表达式

过滤条件可以嵌套，并使用布尔表达式组合任意`AND`和`OR`：

```graphql
{
  users(where: {OR: [
    {name_not_in: ["Karl", "Viggo"]},
  	{AND: [{id: "1"}, {name: "Karl"}]}
  ]}) {
    name
  }
}

```


同一级别的两个过滤条件是显式的`AND`，因此上面的查询可以简化为：

```graphql
{
  users(where: {OR: [
    {name_not_in: ["Karl", "Viggo"]},
  	{id: "1", name: "Karl"}
  ]}) {
    name
  }
}
```

## 交叉关系过滤器

在关系数据库中，通常基于相关表中的列进行过滤。在OpenCRUD中，这个概念称为关系过滤器。以下查询检索与具有id的帖子相关的所有用户`1`。

```graphql
{
  users(where:{posts_some:{id: "1"}}){
    name
  }
}
```

通过反向查询可以实现相同的结果：

```graphql
{
  post(where: {id: "1"}) {
    author {
      name
    }
  }
}
```

关系过滤器与普通过滤器具有相同的功能，可以使用树修改器之一：

* every
* none
* some

```graphql
{
  every: users(where:{posts_every:{id: "1"}}){name}
  none: users(where:{posts_none:{id: "1"}}){name}
  some: users(where:{posts_some:{id: "1"}}){name}
}
```
