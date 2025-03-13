---
lab:
  title: 了解 Azure Synapse 数据资源管理器
  module: Explore fundamentals of real-time analytics
---

# 了解 Azure Synapse 数据资源管理器

> 注意：由于产品更改，本实验室的“创建数据库并引入数据”部分存在一些已知问题。 我们正在努力解决这些问题。

在此练习中，你将使用 Azure Synapse 数据资源管理器分析时序数据。

完成本实验室大约需要 25 分钟。

## 准备工作

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

## 预配 Synapse Analytics 工作区

> 提示：如果你在之前的练习中已经有了Azure Synapse 工作区，那么跳过这一节，直接进入[创建一个数据资源管理器池](#create-a-data-explorer-pool) .

1. 访问 [https://portal.azure/com](https://portal.azure.com?azure-portal=true) 以打开 Azure 门户，然后使用与你的 Azure 订阅关联的凭据登录。

    > 注意：确保使用右上方用户 ID 下显示的包含订阅的目录。 如果没有，请选择用户图标并切换目录。

1. 在 Azure 门户的“主页”上，使用“+ 创建资源”图标创建一个新资源。
1. 搜索“Azure Synapse Analytics”，并创建一个新的 Azure Synapse Analytics 资源，使其包含以下设置：
    - **订阅**：Azure 订阅
        - 资源组：创建一个具有合适名称的新资源组，如名为“synapse-rg”
        - 受管理资源组：输入适当的名称，例如“synapse-managed-rg”。
    - 工作区名称：输入一个唯一的工作区名称，例如“synapse-ws-<your_name>”。
    - 区域：选择任何可用区域。
    - 选择 Data Lake Storage Gen 2：从订阅
        - 帐户名：新建一个具有唯一名称的帐户，例如“datalake<your_name>”。
        - 文件系统名称：新建一个具有唯一名称的文件系统，例如“fs<your_name>”。

    > 注意：Synapse Analytics 工作区需要 Azure 订阅中的两个资源组；一个用于显式创建的资源，另一个用于服务使用的托管资源。 它还需要一个用于存储数据、脚本和其他项目的 Data Lake Storage 帐户。

1. 输入这些详细信息后，选择“审阅并创建”，然后选择“创建”来创建工作区。
1. 等待工作区的创建 - 此操作可能需要约 5 分钟。
1. 部署完成后，转到创建的资源组，并注意它包含你的 Synapse Analytics 工作区和一个 Data Lake Storage 帐户。
1. 选择 Synapse 工作区，并在其“概述”页的“打开 Synapse Studio”卡中选择“打开”，在新浏览器选项卡中打开 Synapse Studio。Synapse Studio 是一个基于 Web 的界面，可用于处理 Synapse Analytics 工作区。
1. 在 Synapse Studio 左侧，使用 &rsaquo;&rsaquo; 图标展开菜单，这将显示 Synapse Studio 中用于管理资源和执行数据分析任务的不同页面。

## 创建数据资源管理器池

1. 在 Synapse Studio 中，选择“管理”页。
1. 选择“数据资源管理器池”选项卡，然后使用“&#65291; 新建”图标，新建一个具有以下设置的新池：
    - 数据资源管理器池名称：dxpool
    - 工作负载：计算优化
    - 大小：特小型（2 核）
1. 选择“下一步: 其他设置 >”并启用“流式引入”设置，这使数据资源管理器能够从流式处理源（如 Azure 事件中心）引入新数据。
1. 选择“查看并创建”以创建数据资源管理器池，然后等待它部署完成（可能需要 15 分钟或更长时间 - 状态将从“正在创建”更改为“联机”）。

## 创建数据库并引入数据

1. 在 Synapse Studio 中，选择“数据”页。
1. 确保选中“工作区”选项卡，并在必要时选择页面左上角的 &#8635; 图标以刷新视图，以便列出数据资源管理器数据库  。
1. 展开“数据资源管理器数据库”并验证是否已列出 dxpool。
1. 在“数据”窗格中，使用 &#65291; 图标在 dxpool 池中创建一个名称为 iot-data 的新数据资源管理器数据库    。
1. 等待创建数据库时，从 [https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv](https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/streaming/data/devices.csv?azure-portal=true) 下载 devices.csv，将其保存在本地计算机上的任一文件夹中。
1. 在 Synapse Studio 中，等待创建数据库（如有必要），然后在新的“iot-data”数据库的“...”菜单中，选择“在 Azure 数据资源管理器中打开”。
1. 在包含 Azure 数据资源管理器的新浏览器选项卡中的“数据”选项卡上，选择“引入新数据”。
1. 在“目标”页中，选择以下设置：
    - 群集：Azure Synapse 工作区中的 dxpool 数据资源管理器池
    - 数据库：iot-data
    - 表：创建名为“设备”的新表
1. 选择“下一步: 源”，在“源”页上，选择以下选项：
    - 源类型：文件
    - 文件：从本地计算机上传 devices.csv 文件。
1. 选择“下一步: 架构”，在“架构”页上，确保以下设置正确：
    - 压缩类型：未压缩
    - 数据格式：CSV
    - 忽略第一条记录：已选择
    - 映射：devices_mapping
1. 确保列数据类型已正确标识为“时间 (datetime)”、“设备 (string)”和“值 (long)”。 然后选择“下一步: 开始引入”。
1. 引入完成后，选择“关闭”。
1. 在 Azure 数据资源管理器的“查询”选项卡上，确保选中“iot-data”数据库，然后在“查询”窗格中输入以下查询。

    ```kusto
    devices
    ```

1. 在工具栏上，选择“&#9655; 运行”来运行查询，并检查结果，结果应该如下所示：

    | 时间 | 设备 | 值 |
    | --- | --- | --- |
    | 2022-01-01T00:00:00Z | Dev1 | 7 |
    | 2022-01-01T00:00:01Z | Dev2 | 4 |
    | ... | ... | ... |

    如果结果与此匹配，则表明你已成功从文件中的数据创建“设备”表。

    > 提示：在本示例中，从文件导入了非常少量的批处理数据，这适用于本练习的目的。 实际上，可以使用数据资源管理器分析更大的数据量；并且，由于启用了流式引入，因此还可以将数据资源管理器配置为将数据从流式处理源（如 Azure 事件中心）引入到数据中。

## 使用 Kusto 查询语言查询 Synapse Studio 中的表

1. 关闭 Azure 数据资源管理器浏览器选项卡并返回到包含 Synapse Studio 的选项卡。
1. 在“数据”页上，展开“iot-data”数据库及其“表”文件夹。 然后在“设备”表的“...”菜单中，选择“新建 KQL 脚本” > “使用 1000 行”。
1. 查看生成的查询及其结果。 查询应包含以下代码：

    ```kusto
    devices
    | take 1000
    ```

    查询结果包含前 1000 行数据。

1. 按照以下方式更改查询：

    ```kusto
    devices
    | where Device == 'Dev1'
    ```

1. 选择“&#9655; 运行”以运行查询。 然后查看结果，其中应仅包含“Dev1”设备的行。

1. 按照以下方式更改查询：

    ```kusto
    devices
    | where Device == 'Dev1'
    | where Time > datetime(2022-01-07)
    ```

1. 运行查询并查看结果，其中应仅包含“Dev1”设备晚于 2022 年 1 月 7 日的行。

1. 按照以下方式更改查询：

    ```kusto
    devices
    | where Time between (datetime(2022-01-01 00:00:00) .. datetime(2022-07-01 23:59:59))
    | summarize AvgVal = avg(Value) by Device
    | sort by Device asc
    ```

1. 运行查询并查看结果，其中应包含 2022 年 1 月 1 日至 1 月 7 日之间记录的平均设备值（按设备名称的升序）。

1. 关闭“KQL 查询”选项卡，放弃所做的更改。

## 删除 Azure 资源

你已完成对 Azure Synapse Analytics 的探索，现在应删除已创建的资源，以避免产生不必要的 Azure 成本。

1. 关闭 Synapse Studio 浏览器选项卡，而不保存任何更改，然后返回 Azure 门户。
1. 在 Azure 门户的“主页”上，选择“资源组”。
1. 选择 Synapse Analytics 工作区的资源组（不是受管理资源组），并确认它包含 Synapse 工作区、存储帐户和工作区的数据资源管理器池（如果你已完成上一练习，则还会包含 Spark 池）。
1. 在资源组的“概述”页的顶部，选择“删除资源组”。
1. 输入资源组名称以确认要删除该资源组，然后选择“删除”。

    几分钟后，你的 Azure Synapse 工作区及其关联的受管理工作区将被删除。
