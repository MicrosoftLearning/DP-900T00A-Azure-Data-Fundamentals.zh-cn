---
lab:
  title: 了解 Azure Cosmos DB
  module: Explore fundamentals of Azure Cosmos DB
---
# <a name="explore-azure-cosmos-db"></a>了解 Azure Cosmos DB

在本练习中，你将在 Azure 订阅中预配 Azure Cosmos DB 数据库，并探索使用它来存储非关系数据的各种方法。

完成本实验室大约需要 15 分钟。

## <a name="before-you-start"></a>开始之前

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

## <a name="create-a-cosmos-db-account"></a>创建 Cosmos DB 帐户

To use Cosmos DB, you must provision a Cosmos DB account in your Azure subscription. In this exercise, you'll provision a Cosmos DB account that uses the core (SQL) API.

1. In the Azure portal, select <bpt id="p1">**</bpt>+ Create a resource<ept id="p1">**</ept> at the top left, and search for <bpt id="p2">*</bpt>Azure Cosmos DB<ept id="p2">*</ept>.  In the results, select <bpt id="p1">**</bpt>Azure Cosmos DB<ept id="p1">**</ept> and select  <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. 在“核心(SQL) - 推荐”框中，选择“创建”。
1. 输入以下详细信息，然后选择“查看 + 创建”：
    - <bpt id="p1">**</bpt>Subscription<ept id="p1">**</ept>: If you're using a sandbox, select <bpt id="p2">*</bpt>Concierge Subscription<ept id="p2">*</ept>. Otherwise, select your Azure subscription.
    - 资源组：如果使用沙盒，请选择现有资源组（其名称类似于 learn-xxxx...）。否则，请使用所选的名称创建一个新资源组。
    - **帐户名**：输入唯一的名称
    -               位置：选择任何建议的位置
    - **容量模式**预配吞吐量
    - **应用免费分级折扣**：如果可用，请选择“应用”
    - **限制总帐户吞吐量**：未选择
1. 验证配置后，选择“创建”。
1. Wait for deployment to complete. Then go to the deployed resource.

## <a name="create-a-sample-database"></a>创建示例数据库

              在整个过程中，关闭门户中显示的任何提示。

1. 在新 Cosmos DB 帐户的页面上，在左侧窗格中选择“数据资源管理器”。
1. 在“数据资源管理器”页中，选择“启动快速入门”。
1. 在“新建容器”选项卡中，查看示例数据库的预填充设置，然后选择“确定”。
1. 在屏幕底部的面板中观察状态，直到“SampleDB”数据库及其“SampleContainer”容器已创建完成（这可能需要一分钟左右的时间）。

## <a name="view-and-create-items"></a>查看和创建项

1. In the Data Explorer page, expand the <bpt id="p1">**</bpt>SampleDB<ept id="p1">**</ept> database and the <bpt id="p2">**</bpt>SampleContainer<ept id="p2">**</ept> container, and select <bpt id="p3">**</bpt>Items<ept id="p3">**</ept> to see a list of items in the container. The items represent addresses, each with a unique id and other properties.
1. 选择列表中的任意项，查看以 JSON 形式表示的项数据。
1. 在页面顶部，选择“新建项目”以创建新的空白项目。
1. 按如下所示修改新项的 JSON 形式，然后选择“保存”。

    ```json
    {
        "address": "1 Any St.",
        "id": "123456789"
    }
    ```

1. 保存新项后，请注意，将自动添加其他元数据属性。

## <a name="query-the-database"></a>查询数据库

1. 在“数据资源管理器”页中，选择“新建 SQL 查询”图标。
1. 在 SQL 查询编辑器中，查看默认查询 (`SELECT * FROM c`)，并使用“执行查询”按钮运行该查询。
1. 查看结果，其中包括所有项的完整 JSON 表示形式。
1. 按照以下方式更改查询：

    ```sql
    SELECT c.id, c.address
    FROM c
    WHERE CONTAINS(c.address, "Any St.")
    ```

1. 使用“执行查询”按钮运行修订后的查询并查看结果，其中包括具有包含文本“Any St.”的“地址”字段的任何项的 JSON 实体。
1. 关闭 SQL 查询编辑器，放弃更改。

    You've seen how to create and query JSON entities in a Cosmos DB database by using the data explorer interface in the Azure portal. In a real scenario, an application developer would use one of the many programming language specific software development kits (SDKs) to call the core (SQL) API and work with data in the database.

> 提示：如果已完成浏览 Azure Cosmos DB，则可以删除在本练习中创建的资源组。
