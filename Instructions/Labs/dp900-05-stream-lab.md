---
lab:
  title: 探索 Azure 流分析
  module: Explore fundamentals of real-time analytics
---

# <a name="explore-azure-stream-analytics"></a>探索 Azure 流分析

在本练习中，你将在 Azure 订阅中预配 Azure 流分析作业，并使用它来处理实时数据流。

完成本实验室大约需要 15 分钟。

## <a name="before-you-start"></a>开始之前

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

## <a name="create-azure-resources"></a>创建 Azure 资源

1. 使用 Azure 订阅凭据在 [Azure 门户](https://portal.azure.com)中登录到 Azure 订阅。

1. 使用页面顶部搜索栏右侧的 [\>_] 按钮在 Azure 门户中新建 Cloud Shell，在出现提示时选择 Bash 环境并创建存储。 Cloud Shell 在 Azure 门户底部的窗格中提供命令行界面，如下所示：

    ![具有 Cloud Shell 窗格的 Azure 门户](./images/cloud-shell.png)

1. 在 Azure Cloud Shell 中，输入以下命令以下载此练习所需的文件。

    ```bash
    git clone https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals dp-900
    ```

1. 等待命令完成，然后输入以下命令将当前目录更改为包含此练习文件的文件夹。

    ```bash
    cd dp-900/streaming
    ```

1. 输入以下命令，以运行创建本练习中将需要的 Azure 资源的脚本。

    ```bash
    bash setup.sh
    ```

    等待脚本运行并执行以下操作：

    1. 安装创建资源所需的 Azure CLI 扩展（可忽略有关实验性扩展的任何警告）
    1. 标识提供用于本练习的 Azure 资源组。
    1. 创建 Azure IoT 中心资源，该资源将用于从模拟设备接收数据流。
    1. 创建 Azure 存储帐户，该帐户将用于存储已处理的数据。
    1. 创建 Azure 流分析作业，该作业将实时处理传入的设备数据，并将结果写入存储帐户。

## <a name="explore-the-azure-resources"></a>探索 Azure 资源

1. 在 [Azure 门户](https://portal.azure.com?azure-portal=true)的主页上，选择“资源组”以查看订阅中的资源组。 这应包括安装脚本标识的 learn-xxxxxxxxxxxxxxxxx... 资源组**。
2. 选择 learn-xxxxxxxxxxxxxxxxx... 资源组，并查看它所包含的资源，这些资源应包括**：
    - 名为 iothubxxxxxxxxxxxxx 的 IoT 中心，用于接收传入的设备数据****。
    - 名为 storexxxxxxxxxxxx 的存储帐户，将向其中写入数据处理结果****。
    - 名为 streamxxxxxxxxxxxxx 的流分析作业，将用于处理流数据****。

    如果这三种资源都未列出，请单击“&#8635; 刷新”按钮，直到它们出现为止。

    > 注意：如果使用的是学习沙盒，则资源组可能还包含名为 cloudshellxxxxxxxx 的另一个存储帐户，该帐户用于存储用于运行安装脚本的 Azure Cloud Shell 的数据****。 

3. 选择 streamxxxxxxxxxxxxx 流分析作业并在其“概述”页上查看信息，请注意以下详细信息**：
    - 该作业包含一个名为 iotinput 的输入和一个名为 bloboutput 的输出。 它们引用了 IoT 中心和安装脚本创建的存储帐户。
    - 该作业包含一个查询，该查询从 iotinput 输入读取数据，并通过计算每 10 秒处理的消息数来聚合该数据；将结果写入 bloboutput 输出。

## <a name="use-the-resources-to-analyze-streaming-data"></a>使用资源分析流数据

1. 在流分析作业的“概述”页顶部，选择“&#9655; 开始”按钮，然后在“开始作业”窗格中，选择“开始”以开始作业。
2. 等待流作业成功开始的通知。
3. 切换回 Azure Cloud Shell，然后输入以下命令来模拟将数据发送到 IoT 中心的设备。

    ```
    bash iotdevice.sh
    ```

4. 等待模拟开始，该操作将由如下输出指示：

    ```
    Device simulation in progress: 6%|#    | 7/120 [00:08<02:21, 1.26s/it]
    ```

5. 运行模拟时，返回 Azure 门户，返回 learn-xxxxxxxxxxxxxxxxx... 资源组页面，然后选择 storexxxxxxxxxxxx 存储帐户 ****。
6. 在存储帐户边栏选项卡左侧的窗格中，选择“容器”选项卡。
7. 打开“数据”容器。
8. 在“数据”容器中，在文件夹层次结构上导航，其中包括当前年份的文件夹，以及月份、日期和小时的子文件夹。
9. 在小时文件夹中，请注意已创建的文件，该文件的名称应类似于 0_xxxxxxxxxxxxxxxx.json。
10. 在文件的“...”菜单（位于文件详细信息右侧）上选择“编辑”，然后查看文件的内容；其中应包含每 10 秒的 JSON 记录，显示从 IoT 设备接收的消息数，如下所示 ：

    ```
    {"starttime":"2021-10-23T01:02:13.2221657Z","endtime":"2021-10-23T01:02:23.2221657Z","device":"iotdevice","messages":2}
    {"starttime":"2021-10-23T01:02:14.5366678Z","endtime":"2021-10-23T01:02:24.5366678Z","device":"iotdevice","messages":3}
    {"starttime":"2021-10-23T01:02:15.7413754Z","endtime":"2021-10-23T01:02:25.7413754Z","device":"iotdevice","messages":4}
    ...
    ```

11. 使用“&#8635; 刷新”按钮刷新文件，请注意，当流分析作业实时处理从设备流式传输到 IoT 中心的设备数据时，其他结果会写入到该文件。
12. 返回 Azure Cloud Shell 并等待设备模拟完成（应运行大约 3 分钟）。
13. 返回 Azure 门户，再次刷新文件，以查看在模拟过程中生成的完整结果集。
14. 返回 learn-xxxxxxxxxxxxxxxxx... 资源组，然后重新打开 streamxxxxxxxxxxxxx 流分析作业 ****。
15. 在流分析作业页的顶部，使用“&#11036; 停止”按钮停止作业，并在出现提示时进行确认。

> 注意：如果已完成流式处理解决方案，请删除在本练习中创建的资源组。
