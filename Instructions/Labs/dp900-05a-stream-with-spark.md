---
lab:
  title: 探索 Azure Synapse Analytics 中的 Spark 流式处理
  module: Explore fundamentals of real-time analytics
---

# 探索 Azure Synapse Analytics 中的 Spark 流式处理

在此练习中，你将使用 Spark 结构化流和 Azure Synapse Analytics 中的增量表来处理流数据。

完成本实验室大约需要 15 分钟。

## 开始之前

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

## 预配 Synapse Analytics 工作区

要使用 Synapse Analytics，必须在 Azure 订阅中预配一个 Synapse Analytics 工作区资源。

1. 访问 [Azure 门户](https://portal.azure.com?azure-portal=true)并将其打开，然后使用与你的 Azure 订阅关联的凭据登录。

    > 注意：确保使用右上方用户 ID 下显示的包含你自己的订阅的目录。 如果没有，请选择用户图标并切换目录。

2. 在 Azure 门户的“主页”上，使用“+ 创建资源”图标创建一个新资源。
3. 搜索“Azure Synapse Analytics”，并创建一个新的 Azure Synapse Analytics 资源，使其包含以下设置：
    - **订阅**：Azure 订阅
        - 资源组：创建一个具有合适名称的新资源组，如名为“synapse-rg”
        - 受管理资源组：输入适当的名称，例如“synapse-managed-rg”。
    - 工作区名称：输入一个唯一的工作区名称，例如“synapse-ws-<your_name>”。
    - 区域：选择任何可用区域。
    - 选择 Data Lake Storage Gen 2：从订阅
        - 帐户名：新建一个具有唯一名称的帐户，例如“datalake<your_name>”。
        - 文件系统名称：新建一个具有唯一名称的文件系统，例如“fs<your_name>”。

    > 注意：Synapse Analytics 工作区需要 Azure 订阅中的两个资源组；一个用于显式创建的资源，另一个用于服务使用的托管资源。 它还需要一个用于存储数据、脚本和其他项目的 Data Lake Storage 帐户。

4. 输入这些详细信息后，选择“审阅并创建”，然后选择“创建”来创建工作区。
5. 等待工作区的创建 - 此操作可能需要约 5 分钟。
6. 部署完成后，转到创建的资源组，并注意它包含你的 Synapse Analytics 工作区和一个 Data Lake Storage 帐户。
7. 选择 Synapse 工作区，并在其“概述”页的“打开 Synapse Studio”卡中选择“打开”，在新浏览器选项卡中打开 Synapse Studio。Synapse Studio 是一个基于 Web 的界面，可用于处理 Synapse Analytics 工作区。
8. 在 Synapse Studio 左侧，使用 &rsaquo;&rsaquo; 图标展开菜单，这将显示 Synapse Studio 中用于管理资源和执行数据分析任务的不同页面，如下所示：

    ![Synapse Studio](images/synapse-studio.png)

## 创建 Spark 池

若要使用 Spark 来处理流数据，需要将 Spark 池添加到 Azure Synapse 工作区。

1. 在 Synapse Studio 中，选择“管理”页。
2. 选择“Apache Spark 池”选项卡，然后使用“+ 新建”图标，新建一个具有以下设置的 Spark 池：
    - Apache Spark 池名称：sparkpool
    - 节点大小系列：内存优化
    - 节点大小：小(4 个 vCore/32 GB)
    - 自动缩放：已启用
    - 节点数：3----3
3. 查看并创建 Spark 池，然后等待它部署完成（可能需要几分钟时间）。

## 探索流处理

若要探索如何使用 Spark 进行流处理，将使用包含 Python 代码和注释的笔记本，以帮助使用 Spark 结构化流和增量表执行一些基本的流处理。

1. 将[结构化流和 Delta Tables.ipynb](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/Spark%20Structured%20Streaming%20and%20Delta%20Tables.ipynb) 笔记本下载到本地计算机（如果该笔记本在浏览器中以文本文件的格式打开，请将其保存到本地文件夹；请谨慎将其保存为结构化流和 Delta Tables.ipynb，而不是 .txt 文件）
2. 在 Synapse Studio 中，选择“开发”页。
3. 在“&#65291;”菜单上，选择“&#8612; 导入”，然后选择本地计算机上的“结构化流和 Delta Tables.ipynb”文件。
4. 按照笔记本中的说明将其附加到 Spark 池，并运行其中包含的代码单元，以探索使用 Spark 进行流处理的各种方法。

## 删除 Azure 资源

> 注意：如果打算完成使用 Azure Synapse Analytics 的其他练习，可以跳过本部分。 否则，请按照以下步骤避免不必要的 Azure 花销。

1. 关闭 Synapse Studio 浏览器选项卡，而不保存任何更改，然后返回 Azure 门户。
1. 在 Azure 门户的“主页”上，选择“资源组”。
1. 选择 Synapse Analytics 工作区的资源组（不是受管理资源组），并确认它包含 Synapse 工作区、存储帐户和工作区的数据资源管理器池（如果你已完成上一练习，则还会包含 Spark 池）。
1. 在资源组的“概述”页的顶部，选择“删除资源组”。
1. 输入资源组名称以确认要删除该资源组，然后选择“删除”。

    几分钟后，你的 Azure Synapse 工作区及其关联的受管理工作区将被删除。
