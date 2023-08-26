---
lab:
  title: 探索 Microsoft Fabric 中的数据分析
  module: Explore fundamentals of large-scale data analytics
---

# 探索 Microsoft Fabric 中的数据分析

在本练习中，你将探索 Microsoft Fabric 湖屋中的数据引入和分析。

完成本实验室大约需要 25 分钟。

> 注意：完成本练习需要 Microsoft Fabric 许可证。 有关如何启用免费 Fabric 试用版许可证的详细信息，请参阅 [Fabric 入门](https://learn.microsoft.com/fabric/get-started/fabric-trial)。 执行此操作需要 Microsoft 学校或工作帐户 。 如果没有，可以[注册 Microsoft Office 365 E3 或更高版本的试用版](https://www.microsoft.com/microsoft-365/business/compare-more-office-365-for-business-plans)。

## 创建工作区

在 Fabric 中处理数据之前，在已启用的 Fabric 试用版中创建工作区。

1. 在 `https://app.fabric.microsoft.com` 登录到 [Microsoft Fabric](https://app.fabric.microsoft.com)。
2. 在左侧菜单栏中，选择“工作区”（图标类似于 &#128455;）。
3. 新建一个工作区并为其指定名称，并在“高级”部分选择包含 Fabric 容量（试用版、高级版或 Fabric）的许可模式  。
4. 打开新工作区时，它应为空。

    ![Power BI 中空工作区的屏幕截图。](./images/new-workspace.png)

## 创建湖屋

有了工作区后，可在门户中切换到数据工程体验，并为数据文件创建一个数据湖屋。

1. 在门户的左下角，切换到“数据工程”体验。

    ![体验切换器菜单的屏幕截图。](./images/fabric-switcher.png)

    数据工程主页包含用于创建常用数据工程资产的磁贴。

2. 在“数据工程”主页中，使用所选名称创建一个新的湖屋 。

    大约一分钟后，一个新的湖屋创建完成：

    ![新湖屋的屏幕截图。](./images/new-lakehouse.png)

3. 查看新的湖屋，并注意使用左侧的湖屋资源管理器窗格可浏览湖屋中的表和文件：
    - Tables 文件夹包含可以使用 SQL 查询的表。 Microsoft Fabric 湖屋中的表基于 Apache Spark 中常用的开源 Delta Lake 文件格式。
    - Files 文件夹包含湖屋的 OneLake 存储中未与托管增量表关联的数据文件。 还可以在此文件夹中创建快捷方式，以引用存储在外部的数据。

    目前，湖屋中没有表或文件。

## 引入数据

引入数据的一种简单方法是使用管道中的“复制数据”活动从源中提取数据并将其复制到湖屋中的文件。

1. 在湖屋的主页上的“获取数据”菜单中选择“新建数据管道”，并创建名为“引入销售数据”的新数据管道   。
1. 在“复制数据”向导的“选择数据源”页上选择“Wide World Importers 的零售数据模型”示例数据集  。

    ![“选择数据源”页的屏幕截图。](./images/choose-data-source.png)

1. 选择“下一步”，并在“连接到数据源”页上查看数据源中的表 。
1. 选择包含产品记录的 dimension_stock_item 表。 然后选择“下一步”以跳转至“选择数据目标”页 。
1. 在“选择数据目标”页上，选择现有湖屋。 然后，选择“下一步”。
1. 设置以下数据目标选项，然后选择“下一步”：
    - **根文件夹**：Tables
    - **加载设置**：加载到新表
    - **目标表名称**：dimension_stock_item
    - **列映射**：保持默认映射不变
    - **启用分区**：未选中
1. 在“查看 + 保存”页上，确保选中“立即开始数据传输”选项，然后选择“保存 + 运行”  。

    将创建一个包含“复制数据”活动的新管道，如下所示：

    ![包含“复制数据”活动的管道的屏幕截图。](./images/copy-data-pipeline.png)

    管道开始运行时，可以在管道设计器下的“输出”窗格中监视其状态。 使用 &#8635;（刷新）图标刷新状态，并等待它成功。

1. 在左侧的中心菜单栏中，选择你的湖屋。
1. 在主页上的“湖屋资源管理器”窗格中展开“Tables”并验证是否已创建 dimension_stock_item 表   。

    > **注意**：如果新表被列为无法识别的表，请使用湖屋工具栏中的“刷新”按钮刷新视图。

1. 选择 dimension_stock_item 表以查看其内容。

    ![dimension_stock_item 表的屏幕截图。](./images/dimProduct.png)

## 查询湖屋中的数据

将数据引入湖屋中的表后，可以使用 SQL 对其进行查询。

1. 在湖屋页面的右上角切换到湖屋的 SQL 终结点。

    ![SQL 终结点菜单的屏幕截图。](./images/endpoint-switcher.png)

1. 在工具栏中选择“新建 SQL 查询”。 然后在查询编辑器中输入以下 SQL 代码：

    ```sql
    SELECT Brand, COUNT(StockItemKey) AS Products
    FROM dimension_stock_item
    GROUP BY Brand
    ```

1. 选择 &#9655;（“运行”）按钮以运行查询并查看结果，结果应显示有两个品牌值（“N/A”和“Northwind”），并显示每个品牌值中的产品数 。

    ![SQL 查询的屏幕截图。](./images/sql-query.png)

## 可视化湖屋中的数据

Microsoft Fabric 湖屋将所有表整理至数据模型中，该数据模型可用于创建可视化效果和报表。

1. 在页面左下角的“浏览”窗格下选择“模型”选项卡，查看湖屋中表（此例中只有一个表）的数据模型 。

    ![Fabric 湖屋中模型页的屏幕截图。](./images/fabric-model.png)

1. 在工具栏中，选择“新建报表”以打开包含 Power BI 报表设计器的新浏览器选项卡。
1. 请在报表设计器中执行以下操作：
    1. 在“数据”窗格中，展开 dimension_stock_item 表，然后选择“Brand”和“StockItemKey”字段   。
    1. 在“可视化效果”窗格中选择堆积条形图可视化效果（列表中的第一个效果） 。 然后确保 Y 轴包含 Brand 字段，并将 X 轴 中的聚合更改为 Count，使其包含 StockItemKey 的计数字段    。 最后在报表画布中调整可视化效果的大小以填充可用空间。

        ![Power BI 报表的屏幕截图。](./images/fabric-report.png)

    > **提示**：可以使用 >> 图标隐藏报表设计器窗格，以便更清楚地查看报表。

1. 在“文件”菜单上选择“保存”，将报表另存为 Fabric 工作区中的品牌数量报表  。

    现在可以关闭包含该报表的浏览器选项卡，返回到湖屋。 可以在 Microsoft Fabric 门户的工作区页面中找到报表。

## 清理资源

如果已完成 Microsoft Fabric 探索，则可以删除为此练习创建的工作区。

1. 在左侧栏中，选择工作区的图标以查看其包含的所有项。
2. 在工具栏上的“...”菜单中，选择“工作区设置” 。
3. 在“其他”部分中，选择“删除此工作区” 。
