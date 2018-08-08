# 关系

* 覆盖的领域
* 关注api，不包含实现以及运行时的特性
* SDL

## 覆盖的领域

该规范描述了适用于关系数据库的灵活GraphQL API的所有方面

## 关注api，不包含实现以及运行时的特性

OpenCrud是GraphQL API的规范集合，旨在与特定的数据库技术配合使用。OpenCRUD关注API表面，而不是实现。因此，OpenCRUD的两个实现可以选择以不同的方式存储数据，但是通过OpenCRUD API与数据交互的应用程序将无法区分。

## SDL

本规范中使用的示例显示了为特定数据模型生成的最终模式。在所有示例中，SDL表示法用于定义数据模型。SDL的好处在于它与数据库无关，因此我们可以在所有支持的数据库中使用相同的表示法。

在本规范的示例SDL中使用时，以下指令具有特殊含义：

- `@unique`：该字段具有唯一约束
- `@relation`：指定两个字段之间的关系

## Queries

### [Queries: Top level](2-2-queries/2-2-1-toplevel-zh.md)

### [Queries: Relations](2-2-queries/2-2-2-relations-zh.md)

### [Queries: Filters](2-2-queries/2-2-3-filters-zh.md)

### [Queries: Aggregations](2-2-queries/2-2-4-aggregations-zh.md)

## Mutations

### [Mutations: CRUD](2-3-mutations/2-3-1-crud-zh.md)

### [Mutations: Batch](2-3-mutations/2-3-2-batch-zh.md)

### [Mutations: Nested](2-3-mutations/2-3-3-nested-zh.md)
