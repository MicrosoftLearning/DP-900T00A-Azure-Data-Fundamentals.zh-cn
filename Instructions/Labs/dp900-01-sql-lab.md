---
lab:
  title: 探索 Azure SQL 数据库
  module: Explore relational data in Azure
---

# <a name="explore-azure-sql-database"></a>探索 Azure SQL 数据库

在本练习中，你将在 Azure 订阅中预配 Azure SQL 数据库资源，然后使用 SQL 查询关系数据库中的表。

本练习大约需要 15 分钟才能完成。

## <a name="before-you-start"></a>准备工作

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

## <a name="provision-an-azure-sql-database-resource"></a>预配 Azure SQL 数据库资源

1. 在 [Azure 门户](https://portal.azure.com?azure-portal=true)的左上角选择“&#65291; 创建资源”，然后搜索“Azure SQL”。 然后在出现的“Azure SQL”页面中，选择“创建”。

1. 查看可用的 Azure SQL 选项，然后在“SQL 数据库”磁贴中，确保选中“单一数据库”并选择“创建”。

    ![Azure 门户的屏幕截图，其中显示了 Azure SQL 页面。](images//azure-sql-portal.png)

1. 在“创建 SQL 数据库”页上输入以下值，并将所有其他属性保留为默认设置：
    - **订阅**：选择 Azure 订阅。
    - **资源组**：使用你所选择的名称创建新资源组。
    -               数据库名称：AdventureWorks
    -                 **服务器**：选择“新建”，并在任何可用位置创建具有唯一名称的新服务器。 使用“SQL 身份验证”，并指定你的姓名作为服务器管理员登录名和一个适当复杂的密码（请记住密码 - 稍后你将需要它！）
    -               想要使用 SQL 弹性池吗？：否
    - 工作负载环境：开发
    -               计算 + 存储：保持不变
    -               备份存储冗余：本地冗余备份存储

1. 在“创建 SQL 数据库”页上，选择“下一步: 网络 >”，然后在“网络”页上的“网络连接”部分，选择“公共终结点”    。 然后为“防火墙规则”部分中的两个选项选择“是”，以允许从 Azure 服务和当前客户端 IP 地址访问数据库服务器。

1. 选择“下一步: 安全性 >”，并将“启用 Microsoft Defender for SQL”选项设置为“现在不启用”  。

1. 选择“下一步: 其他设置 >”，然后在“其他设置”选项卡上，将“使用现有数据”选项设置为“示例”（这将创建一个示例数据库，你可以稍后进行探索）   。

1. 依次选择“查看 + 创建”、“创建”，以创建 Azure SQL 数据库。

1. 等待部署完成。 然后转到已部署的资源，它应该如下所示：

    ![Azure 门户的屏幕截图，其中显示了 SQL 数据库页面。](images//sql-database-portal.png)

1. 在页面左侧的窗格中，选择“查询编辑器(预览版)”，然后使用为服务器指定的管理员登录名和密码登录。
    
                  如果显示一条表示“不允许使用客户端 IP 地址”的错误消息，请选择消息末尾的“允许列表 IP …”链接以允许访问并尝试再次登录（虽然之前已将自己计算机的客户端 IP 地址添加到防火墙规则中，但查询编辑器可能会从不同的地址进行连接，具体取决于网络配置。）
    
    查询编辑器如下所示：
    
    ![Azure 门户的屏幕截图，其中显示了查询编辑器。](images//query-editor.png)

1. 展开 Tables 文件夹，查看数据库中的表。

1. 在“查询 1”窗格中，输入以下 SQL 代码：

    ```sql
    SELECT * FROM SalesLT.Product;
    ```

1. 选择查询上方的“&#9655;运行”以运行该代码，并查看结果，其中应包括 SalesLT.Product 表中的所有行和列，如下所示 ：

    ![Azure 门户的屏幕截图，其中显示了包含查询结果的查询编辑器。](images//sql-query-results.png)

1. 将 SELECT 语句替换为以下代码，然后选择“&#9655; 运行”以运行新查询并查看结果（其中仅包括 ProductID、Name、ListPrice、ProductCategoryID 列）    ：

    ```sql
    SELECT ProductID, Name, ListPrice, ProductCategoryID
    FROM SalesLT.Product;
    ```

1. 现在尝试以下查询，该查询使用 JOIN 从 SalesLT.ProductCategory 表中获取类别名称：

    ```sql
    SELECT p.ProductID, p.Name AS ProductName,
            c.Name AS Category, p.ListPrice
    FROM SalesLT.Product AS p
    JOIN [SalesLT].[ProductCategory] AS c
        ON p.ProductCategoryID = c.ProductCategoryID;
    ```

1. 关闭查询编辑器窗格，并放弃所做的编辑。

> 提示：如果已完成对 Azure SQL 数据库的探索，可删除在本练习中创建的资源组。
