---
lab:
  title: 使用 Power BI 探索数据可视化的基础知识
  module: Explore fundamentals of data visualization
---

# <a name="explore-fundamentals-of-data-visualization-with-power-bi"></a>使用 Power BI 探索数据可视化的基础知识

在本练习中，你将使用 Microsoft Power BI Desktop 创建包含交互式数据可视化效果的数据模型和报表。

完成本实验室大约需要 20 分钟。

## <a name="before-you-start"></a>开始之前

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

### <a name="install-power-bi-desktop"></a>安装 Power BI Desktop

如果你的 Windows 计算机上尚未安装 Microsoft Power BI Desktop，则可以免费下载和安装。

1. 从 [https://aka.ms/power-bi-desktop](https://aka.ms/power-bi-desktop?azure-portal=true) 下载 Power BI Desktop 安装程序。
1. When the file has downloaded, open it, and use the setup wizard to install Power BI Desktop on your computer. This insatllation may take a few minutes.

## <a name="import-data"></a>导入数据

1. Open Power BI Desktop. The application interface should look similar to this:

    ![显示 Power BI Desktop 开始屏幕的屏幕截图。](images/power-bi-start.png)

    现在，你可以导入报表数据。

1. 在 Power BI Desktop 的欢迎屏幕上，选择“获取数据”，然后在数据源列表中选择“Web”，再选择“连接”。

    ![显示如何在 Power BI 中选择 Web 数据源的屏幕截图。](images/web-source.png)

1. 在“来自 Web”对话框中，输入以下 URL，然后选择“确定”：

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/customers.csv
    ```

1. 在“访问 Web 内容”对话框中，选择“连接”。

1. Verify that the URL opens a dataset containing customer data, as shown below. Then select <bpt id="p1">**</bpt>Load<ept id="p1">**</ept> to load the data into the data model for your report.

    ![显示 Power BI 中显示的客户数据集的屏幕截图。](images/customers.png)

1. 在 Power BI Desktop 主窗口的“数据局”菜单中，选择“获取数据”，然后选择 Web ：

    ![显示 Power BI 中“获取数据”菜单的屏幕截图。](images/get-data.png)

1. 在“来自 Web”对话框中，输入以下 URL，然后选择“确定”：

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/products.csv
    ```

1. 在对话框中，选择“加载”，将此文件中的产品数据加载到数据模型中。

1. 重复上述三个步骤，从以下 URL 导入包含订单数据的第三个数据集：

    ```
    https://github.com/MicrosoftLearning/DP-900T00A-Azure-Data-Fundamentals/raw/master/power-bi/orders.csv
    ```

## <a name="explore-a-data-model"></a>了解数据模型

导入的三个数据表已加载到数据模型中，现在你可以查看并对其进行优化。

1. In Power BI Desktop, on the left-side edge, select the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> tab, and then arrange the tables in the model so you can see them. You can hide the panes on the right side by using the <bpt id="p1">**</bpt><ph id="ph1">&gt;&gt;</ph><ept id="p1">**</ept> icons:

    ![显示 Power BI 中“模型”选项卡的屏幕截图。](images/model-tab.png)

1. 在 orders 表中，选择“Revenue”字段，然后在“属性”窗格中，将其“格式”属性设置为“Currency”：

    ![显示如何在 Power BI 中将 Revenue 格式设置为 Currency 的屏幕截图。](images/revenue-currency.png)

    此步骤将确保收入值在报表可视化效果中显示为货币。

1. In the products table, right-click the <bpt id="p1">**</bpt>Category<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Create hierarchy<ept id="p3">**</ept>. This step creates a hierarchy named <bpt id="p1">**</bpt>Category Hierarchy<ept id="p1">**</ept>. You may need to expand or scroll in the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> table to see this - you can also see it in the <bpt id="p2">**</bpt>Fields<ept id="p2">**</ept> pane:

    ![显示如何在 Power BI 中添加 Category Hierarchy 的屏幕截图。](images/category-hierarchy.png)

1. In the products table, right-click the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field (or open its <bpt id="p2">**</bpt><ph id="ph1">&amp;vellip;</ph><ept id="p2">**</ept> menu) and select <bpt id="p3">**</bpt>Add to hierarchy<ept id="p3">**</ept><ph id="ph2"> &gt; </ph><bpt id="p4">**</bpt>Category Hierarchy<ept id="p4">**</ept>. This adds the <bpt id="p1">**</bpt>ProductName<ept id="p1">**</ept> field to the hierarchy you created previously.
1. In the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, right-click <bpt id="p2">**</bpt>Category Hierarchy<ept id="p2">**</ept> (or open its <bpt id="p3">**</bpt>...<ept id="p3">**</ept> menu) and select <bpt id="p4">**</bpt>Rename<ept id="p4">**</ept>. Then rename the hierarchy to <bpt id="p1">**</bpt>Categorized Product<ept id="p1">**</ept>.

    ![显示如何在 Power BI 中重命名层次结构的屏幕截图。](images/rename-hierarchy.png)

1. 在左侧边缘，选择“数据”选项卡，然后在“字段”窗格中，选择 customers 表。
1. 选择“City”列标题，然后将其“数据类别”属性设置为“City”：

    ![显示如何在 Power BI 中设置数据类别的屏幕截图。](images/data-category.png)

    此步骤将确保将此列中的值解释为城市名称，在你打算包括地图可视化效果时，这很有用。

## <a name="create-a-report"></a>创建报表

Now you're almost ready to create a report. First you need to check some settings to ensure all visualizations are enabled.

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Options and Settings<ept id="p2">**</ept>. Then select <bpt id="p1">**</bpt>Options<ept id="p1">**</ept>, and in the <bpt id="p2">**</bpt>Security<ept id="p2">**</ept> section, ensure that <bpt id="p3">**</bpt>Use Map and Filled Map visuals<ept id="p3">**</ept> is enabled and select <bpt id="p4">**</bpt>OK<ept id="p4">**</ept>.

    ![显示如何在 PowerBI 中设置“使用地图和着色地图视觉对象”属性的屏幕截图。](images/set-options.png)

    此设置确保在报表中能够包括地图可视化效果。

1. 在左侧边缘，选择“报表”选项卡并查看报表设计界面。

    ![显示 Power BI 中“报表”选项卡的屏幕截图。](images/report-tab.png)

1. In the ribbon, above the report design surface, select <bpt id="p1">**</bpt>Text Box<ept id="p1">**</ept> and add a text box containing the text <bpt id="p2">**</bpt>Sales Report<ept id="p2">**</ept> to the report. Format the text to make it bold with a font size of 32.

    ![显示如何在 Power BI 中添加文本框的屏幕截图。](images/text-box.png)

1. 下载文件后，将其打开，然后使用安装向导在计算机上安装 Power BI Desktop。

    ![显示如何在 Power BI 中向报表添加分类产品表的屏幕截图。](images/categorized-products-table.png)

1. 安装可能需要几分钟时间。

    The revenue is formatted as currency, as you specified in the model. However, you didn't specify the number of decimal places, so the values include fractional amounts. It won't matter for the visualizations you're going to create, but you could go back to the <bpt id="p1">**</bpt>Model<ept id="p1">**</ept> or <bpt id="p2">**</bpt>Data<ept id="p2">**</ept> tab and change the decimal places if you wish.

    ![显示报表中包含收入的分类产品表的屏幕截图。](images/revenue-column.png)

1. With the table still selected, in the <bpt id="p1">**</bpt>Visualizations<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Stacked column chart<ept id="p2">**</ept> visualization. The table is changed to a column chart showing revenue by category.

    ![显示报表中包含收入的分类产品的堆积柱形图的屏幕截图。](images/stacked-column-chart.png)

1. 打开 Power BI Desktop。

    ![显示向下钻取以查看类别中的产品的柱形图的屏幕截图。](images/drill-down.png)

1. 应用程序界面应如下所示：
1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>Quantity<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>orders<ept id="p3">**</ept> table and the <bpt id="p4">**</bpt>Category<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>products<ept id="p5">**</ept> table. This step results in another column chart showing sales quantity by product category.
1. 选中新的柱形图后，在“可视化”窗格中选择“饼图”，然后调整饼图大小并将其放置在按类别显示的收入旁边。

    ![显示按类别显示销售数量的饼图的屏幕截图。](images/category-pie-chart.png)

1. Select a blank area of the report, and then in the <bpt id="p1">**</bpt>Fields<ept id="p1">**</ept> pane, select the <bpt id="p2">**</bpt>City<ept id="p2">**</ept> field in the <bpt id="p3">**</bpt>customers<ept id="p3">**</ept> table and then select the <bpt id="p4">**</bpt>Revenue<ept id="p4">**</ept> field in the <bpt id="p5">**</bpt>orders<ept id="p5">**</ept> table. This results in a map showing sales revenue by city. Rearrange and resize the visualizations as needed:

    ![显示按城市显示收入的地图的屏幕截图。](images/revenue-map.png)

1. In the map, note that you can drag, double-click, use a mouse-wheel, or pinch and drag on a touch screen to interact. Then select a specific city, and note that the other visualizations in the report are modified to highlight the data for the selected city.

    ![显示按城市显示收入的地图的屏幕截图，其中突出显示了所选城市的数据。](images/selected-data.png)

1. On the <bpt id="p1">**</bpt>File<ept id="p1">**</ept> menu, select <bpt id="p2">**</bpt>Save<ept id="p2">**</ept>. Then save the file with an appropriate .pbix file name. You can open the file and explore data modeling and visualization further at your leisure.

如果你有 [Power BI 服务](https://www.powerbi.com/?azure-portal=true)订阅，则可以登录到你的帐户并将报表发布到 Power BI 工作区。 
