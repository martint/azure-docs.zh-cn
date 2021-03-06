---
title: 在 Azure Cosmos DB 中查找请求单位 (RU) 费用
description: 了解如何查找针对 Azure Cosmos 容器执行的任何操作所产生的请求单位费用
author: ThomasWeiss
ms.service: cosmos-db
ms.topic: sample
ms.date: 03/21/2019
ms.author: thweiss
ms.openlocfilehash: e3175ee136057c695ceef3cd1976b447a529c803
ms.sourcegitcommit: 8313d5bf28fb32e8531cdd4a3054065fa7315bfd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2019
ms.locfileid: "59053037"
---
# <a name="find-the-request-unit-ru-charge-in-azure-cosmos-db"></a>在 Azure Cosmos DB 中查找请求单位 (RU) 费用

本文介绍如何通过不同的方式，来查找针对 Azure Cosmos 容器执行的任何操作所消耗的[请求单位](request-units.md)。 目前，若要度量这种消耗，可以使用 Azure 门户，或者通过某个 SDK 检查 Azure Cosmos DB 发回的响应。

## <a name="core-api"></a>核心 API

### <a name="use-the-azure-portal"></a>使用 Azure 门户

在 Azure 门户中，目前只能查找 SQL 查询的请求费用。

1. 登录到 [Azure 门户](https://portal.azure.com/)。

1. [创建新的 Azure Cosmos DB 帐户](create-sql-api-dotnet.md#create-account)并在其中植入数据，或选择一个已包含数据的现有帐户。

1. 打开“数据资源管理器”窗格，选择要使用的容器。

1. 单击“新建 SQL 查询”。

1. 输入有效的查询，然后单击“执行查询”。

1. 单击“查询统计信息”，以显示刚刚执行的请求的实际请求费用。

![Azure 门户上的 SQL 查询请求费用屏幕截图](./media/find-request-unit-charge/portal-sql-query.png)

### <a name="use-the-net-sdk-v2"></a>使用 .NET SDK V2

[.NET SDK v2](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)（请参阅[此快速入门](create-sql-api-dotnet.md)了解其用法）返回的对象会公开 `RequestCharge` 属性。

```csharp
ResourceResponse<Document> fetchDocumentResponse = await client.ReadDocumentAsync(
    UriFactory.CreateDocumentUri("database", "container", "itemId"),
    new RequestOptions
    {
        PartitionKey = new PartitionKey("partitionKey")
    });
var requestCharge = fetchDocumentResponse.RequestCharge;

StoredProcedureResponse<string> storedProcedureCallResponse = await client.ExecuteStoredProcedureAsync<string>(
    UriFactory.CreateStoredProcedureUri("database", "container", "storedProcedureId"),
    new RequestOptions
    {
        PartitionKey = new PartitionKey("partitionKey")
    });
requestCharge = storedProcedureCallResponse.RequestCharge;

IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri("database", "container"),
    "SELECT * FROM c",
    new FeedOptions
    {
        PartitionKey = new PartitionKey("partitionKey")
    }).AsDocumentQuery();
while (query.HasMoreResults)
{
    FeedResponse<dynamic> queryResponse = await query.ExecuteNextAsync<dynamic>();
    requestCharge = queryResponse.RequestCharge;
}
```

### <a name="use-the-java-sdk"></a>使用 Java SDK

[Java SDK](https://mvnrepository.com/artifact/com.microsoft.azure/azure-cosmosdb)（请参阅[此快速入门](create-sql-api-java.md)了解其用法）返回的对象会公开 `getRequestCharge()` 方法。

```java
RequestOptions requestOptions = new RequestOptions();
requestOptions.setPartitionKey(new PartitionKey("partitionKey"));

Observable<ResourceResponse<Document>> readDocumentResponse = client.readDocument(String.format("/dbs/%s/colls/%s/docs/%s", "database", "container", "itemId"), requestOptions);
readDocumentResponse.subscribe(result -> {
    double requestCharge = result.getRequestCharge();
});

Observable<StoredProcedureResponse> storedProcedureResponse = client.executeStoredProcedure(String.format("/dbs/%s/colls/%s/sprocs/%s", "database", "container", "storedProcedureId"), requestOptions, null);
storedProcedureResponse.subscribe(result -> {
    double requestCharge = result.getRequestCharge();
});

FeedOptions feedOptions = new FeedOptions();
feedOptions.setPartitionKey(new PartitionKey("partitionKey"));

Observable<FeedResponse<Document>> feedResponse = client
    .queryDocuments(String.format("/dbs/%s/colls/%s", "database", "container"), "SELECT * FROM c", feedOptions);
feedResponse.forEach(result -> {
    double requestCharge = result.getRequestCharge();
});
```

### <a name="use-the-nodejs-sdk"></a>使用 Node.js SDK

[Node.js SDK](https://www.npmjs.com/package/@azure/cosmos)（请参阅[此快速入门](create-sql-api-nodejs.md)了解其用法）返回的对象会公开一个 `headers` 子对象，该对象可映射底层 HTTP API 返回的所有标头。 请求费用显示在 `x-ms-request-charge` 键下。

```javascript
const item = await client
    .database('database')
    .container('container')
    .item('itemId', 'partitionKey')
    .read();
var requestCharge = item.headers['x-ms-request-charge'];

const storedProcedureResult = await client
    .database('database')
    .container('container')
    .storedProcedure('storedProcedureId')
    .execute({
        partitionKey: 'partitionKey'
    });
requestCharge = storedProcedureResult.headers['x-ms-request-charge'];

const query = client.database('database')
    .container('container')
    .items
    .query('SELECT * FROM c', {
        partitionKey: 'partitionKey'
    });
while (query.hasMoreResults()) {
    var result = await query.executeNext();
    requestCharge = result.headers['x-ms-request-charge'];
}
```

### <a name="use-the-python-sdk"></a>使用 Python SDK

[Python SDK](https://pypi.org/project/azure-cosmos/)（请参阅[此快速入门](create-sql-api-python.md)了解其用法）返回的 `CosmosClient` 对象会公开一个 `last_response_headers` 字典，该字典可映射底层 HTTP API 针对上次执行的操作返回的所有标头。 请求费用显示在 `x-ms-request-charge` 键下。

```python
response = client.ReadItem('dbs/database/colls/container/docs/itemId', { 'partitionKey': 'partitionKey' })
request_charge = client.last_response_headers['x-ms-request-charge']

response = client.ExecuteStoredProcedure('dbs/database/colls/container/sprocs/storedProcedureId', None, { 'partitionKey': 'partitionKey' })
request_charge = client.last_response_headers['x-ms-request-charge']
```

## <a name="azure-cosmos-dbs-api-for-mongodb"></a>Azure Cosmos DB 的用于 MongoDB 的 API

请求单位费用由名为 `getLastRequestStatistics` 的自定义[数据库命令](https://docs.mongodb.com/manual/reference/command/)公开。 此命令返回一个文档，其中包含上次执行的操作的名称、其请求费用和持续时间。

### <a name="use-the-azure-portal"></a>使用 Azure 门户

在 Azure 门户中，目前只能查找查询的请求费用。

1. 登录到 [Azure 门户](https://portal.azure.com/)。

1. [创建新的 Azure Cosmos DB 帐户](create-mongodb-dotnet.md#create-a-database-account)并在其中植入数据，或选择一个已包含数据的现有帐户。

1. 打开“数据资源管理器”窗格，选择要使用的集合。

1. 单击“新建查询”。

1. 输入有效的查询，然后单击“执行查询”。

1. 单击“查询统计信息”，以显示刚刚执行的请求的实际请求费用。

![Azure 门户上的 MongoDB 查询请求费用屏幕截图](./media/find-request-unit-charge/portal-mongodb-query.png)

### <a name="use-the-mongodb-net-driver"></a>使用 MongoDB .NET 驱动程序

使用[官方的 MongoDB .NET 驱动程序](https://docs.mongodb.com/ecosystem/drivers/csharp/)（请参阅[此快速入门](create-mongodb-dotnet.md)了解其用法）时，可以通过针对 `IMongoDatabase` 对象调用 `RunCommand` 方法来执行命令。 此方法需要 `Command<>` 抽象类的实现。

```csharp
class GetLastRequestStatisticsCommand : Command<Dictionary<string, object>>
{
    public override RenderedCommand<Dictionary<string, object>> Render(IBsonSerializerRegistry serializerRegistry)
    {
        return new RenderedCommand<Dictionary<string, object>>(new BsonDocument("getLastRequestStatistics", 1), serializerRegistry.GetSerializer<Dictionary<string, object>>());
    }
}

Dictionary<string, object> stats = database.RunCommand(new GetLastRequestStatisticsCommand());
double requestCharge = (double)stats["RequestCharge"];
```

### <a name="use-the-mongodb-java-driver"></a>使用 MongoDB Java 驱动程序

使用[官方的 MongoDB Java 驱动程序](http://mongodb.github.io/mongo-java-driver/)（请参阅[此快速入门](create-mongodb-java.md)了解其用法）时，可以通过针对 `MongoDatabase` 对象调用 `runCommand` 方法来执行命令。

```java
Document stats = database.runCommand(new Document("getLastRequestStatistics", 1));
Double requestCharge = stats.getDouble("RequestCharge");
```

### <a name="use-the-mongodb-nodejs-driver"></a>使用 MongoDB Node.js 驱动程序

使用[官方的 MongoDB Node.js 驱动程序](https://mongodb.github.io/node-mongodb-native/)（请参阅[此快速入门](create-mongodb-nodejs.md)了解其用法）时，可以通过针对 `Db` 对象调用 `command` 方法来执行命令。

```javascript
db.command({ getLastRequestStatistics: 1 }, function(err, result) {
    assert.equal(err, null);
    const requestCharge = result['RequestCharge'];
});
```

## <a name="cassandra-api"></a>Cassandra API

针对 Azure Cosmos DB 的 Cassandra API 执行操作时，请求单位费用将在传入的有效负载中，以名为 `RequestCharge` 的字段形式返回。

### <a name="use-the-net-sdk"></a>使用 .NET SDK

使用 [.NET SDK](https://www.nuget.org/packages/CassandraCSharpDriver/)（请参阅[此快速入门](create-cassandra-dotnet.md)了解其用法）时，可以在 `RowSet` 对象的 `Info` 属性下检索传入的有效负载。

```csharp
RowSet rowSet = session.Execute("SELECT table_name FROM system_schema.tables;");
double requestCharge = BitConverter.ToDouble(rowSet.Info.IncomingPayload["RequestCharge"], 0);
```

### <a name="use-the-java-sdk"></a>使用 Java SDK

使用 [Java SDK](https://mvnrepository.com/artifact/com.datastax.cassandra/cassandra-driver-core)（请参阅[此快速入门](create-cassandra-java.md)了解其用法）时，可以通过针对 `ResultSet` 对象调用 `getExecutionInfo()` 方法来检索传入的有效负载。

```java
ResultSet resultSet = session.execute("SELECT table_name FROM system_schema.tables;");
Double requestCharge = resultSet.getExecutionInfo().getIncomingPayload().get("RequestCharge").getDouble();
```

## <a name="gremlin-api"></a>Gremlin API

### <a name="use-drivers-and-sdk"></a>使用驱动程序和 SDK

Gremlin API 返回的标头将映射到目前由 Gremlin .NET 和 Java SDK 公开的自定义状态特性。 请求费用显示在 `x-ms-request-charge` 键下。

### <a name="use-the-net-sdk"></a>使用 .NET SDK

使用 [Gremlin .NET SDK](https://www.nuget.org/packages/Gremlin.Net/)（请参阅[此快速入门](create-graph-dotnet.md)了解其用法）时，状态特性将显示在 `ResultSet<>` 对象的 `StatusAttributes` 属性下。

```csharp
ResultSet<dynamic> results = client.SubmitAsync<dynamic>("g.V().count()").Result;
double requestCharge = (double)results.StatusAttributes["x-ms-request-charge"];
```

### <a name="use-the-java-sdk"></a>使用 Java SDK

使用 [Gremlin Java SDK](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver)（请参阅[此快速入门](create-graph-java.md)了解其用法）时，可以通过针对 `ResultSet` 对象调用 `statusAttributes()` 方法来检索状态特性。

```java
ResultSet results = client.submit("g.V().count()");
Double requestCharge = (Double)results.statusAttributes().get().get("x-ms-request-charge");
```

## <a name="table-api"></a>表 API

目前，只有 [.NET 标准 SDK](https://www.nuget.org/packages/Microsoft.Azure.Cosmos.Table)（请参阅[此快速入门](create-table-dotnet.md)了解其用法）才能返回表操作的请求单位费用。 `TableResult` 对象公开 `RequestCharge` 属性，针对 Azure Cosmos DB 的表 API 使用该 SDK 时，该 SDK 会填充该属性。

```csharp
CloudTable tableReference = client.GetTableReference("table");
TableResult tableResult = tableReference.Execute(TableOperation.Insert(new DynamicTableEntity("partitionKey", "rowKey")));
if (tableResult.RequestCharge.HasValue) // would be false when using Azure Storage Tables
{
    double requestCharge = tableResult.RequestCharge.Value;
}
```

## <a name="next-steps"></a>后续步骤

请参阅以下文章，了解如何优化请求单位消耗量：

* [在 Azure Cosmos DB 中优化预配的吞吐量成本](optimize-cost-throughput.md)
* [优化 Azure Cosmos DB 中的查询成本](optimize-cost-queries.md)