---
lab:
  title: 探索 Microsoft Fabric 中的实时分析
  module: Explore fundamentals of large-scale data analytics
---

# 探索 Microsoft Fabric 中的实时分析

在本练习中，你将探索 Microsoft Fabric 中的实时分析。

完成本实验室大约需要 25 分钟。

> 注意：需要 Microsoft Fabric 许可证才能完成本练习。 有关如何启用免费 Fabric 试用版许可证的详细信息，请参阅 [Fabric 入门](https://learn.microsoft.com/fabric/get-started/fabric-trial)。 需要 Microsoft 学校或工作帐户才能执行此操作 。 如果没有该帐户，可以[注册 Microsoft Office 365 E3 或更高版本的试用版](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans)。

## 创建工作区

在 Fabric 中处理数据之前，创建一个已启用的 Fabric 试用版的工作区。

1. 在 `https://app.fabric.microsoft.com` 登录到 [Microsoft Fabric](https://app.fabric.microsoft.com)。
2. 在左侧菜单栏中，选择“工作区”（图标类似于 &#128455;）。
3. 新建一个工作区并为其指定名称，并在“高级”部分选择包含 Fabric 容量（试用版、高级版或 Fabric）的许可模式  。
4. 打开新工作区时，它应为空。

    ![Power BI 中空工作区的屏幕截图。](./images/new-workspace.png)

## 创建 KQL 数据库

有了工作区后，可以创建 KQL 数据库来存储实时数据。

1. 在门户的左下角，切换到“实时智能”体验****。

    ![体验切换器菜单的屏幕截图。](./images/fabric-real-time.png)

    实时智能主页包含的磁贴可用于创建实时数据分析的常用资产。

2. 在实时智能主页中，创建一个新的 **Eventhouse**，名称自定。

    ![RTA 编辑器的屏幕截图，其中突出显示了“创建 KQL DB”。](./images/create-kql-db.png)

    Eventhouse 用于对跨项目的数据库进行分组和管理。 一个空的 KQL 数据库会自动以 eventhouse 的名称创建，我们将在本练习的稍后部分向其中添加数据。

## 创建事件流

事件流提供一种可缩放且灵活的方法，可从流式处理源引入实时数据。

1. 在左侧菜单栏中，选择“主页”页面以获取实时智能体验****。
1. 在主页上选择磁贴以按照自己需要的名称创建新的事件流。

    一小段时间后，系统将显示事件流的可视化设计器。

    ![事件流设计器的屏幕截图。](./images/eventstream-designer.png)

    可视化设计器画布显示连接到事件流的源，事件流又连接到目标。

1. 在设计器画布上，在源的“新建源”列表中，选择“示例数据” 。 然后，在“示例数据”窗格中指定名称“taxis”（出租车）并选择“Yellow Taxi”（黄色出租车）示例数据（表示从出租车行程收集的数据）  。 然后选择“添加”  。
1. 在设计器画布下，选择“数据预览”选项卡以预览从源流式传输的数据：

    ![事件流数据预览的屏幕截图。](./images/eventstream-preview.png)

1. 在设计器画布上，在目标的“新建目标”列表中，选择“KQL 数据库” 。 然后在“KQL 数据库”窗格中，指定目标名称“taxi-data”，并选择工作区和 KQL 数据库 。 选择目标表下的“新建”，然后输入表名“taxi-data”********。 然后选择“添加”  。
1. 验证已完成的事件流是否如下所示：

    ![已完成的事件流的屏幕截图。](./images/complete-eventstream.png)

## 查询 KQL 数据库中的实时数据

事件流会持续填充 KQL 数据库中的表，让你能够查询实时数据。

1. 在左侧菜单中心选择 KQL 数据库（或选择工作区，并在工作区中找到 KQL 数据库）。
1. 在通过事件流创建的“taxi-data”表的“...”菜单中选择“查询表”>“过去 24 小时引入的记录”  。

    ![KQL 数据库中“查询表”菜单的屏幕截图。](./images/kql-query.png)

1. 查看查询的结果，该查询应该为类似以下内容的 KQL 查询：

    ```kql
    ['taxi-data']
    | where ingestion_time() between (now(-1d) .. now())
    ```

    结果显示过去 24 小时内从流式处理源引入的所有出租车记录。

1. 将查询编辑器上半部分的所有 KQL 查询代码替换为以下代码：

    ```kql
    // This query returns the number of taxi pickups per hour
    ['taxi-data']
    | summarize PickupCount = count() by bin(todatetime(tpep_pickup_datetime), 1h)
    ```

1. 使用 &#9655;（“运行”）按钮运行查询并查看结果，结果应显示每小时的出租车接送数。

## 清理资源

如果已完成 Microsoft Fabric 中的实时分析探索，则可以删除为此练习创建的工作区。

1. 在左侧栏中，选择工作区的图标以查看其包含的所有项。
2. 在工具栏上的“...”菜单中，选择“工作区设置” 。
3. 在“其他”部分中，选择“删除此工作区” 。
