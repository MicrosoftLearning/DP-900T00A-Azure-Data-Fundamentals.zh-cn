---
lab:
  title: 探索 Azure 存储
  module: Explore Azure Storage for non-relational data
---

# <a name="explore-azure-storage"></a>探索 Azure 存储

在本练习中，你将在 Azure 订阅中预配一个 Azure 存储帐户，并探索可以使用它来存储数据的各种方式。

完成本实验室大约需要 15 分钟。

## <a name="before-you-start"></a>开始之前

需要一个你在其中具有管理级权限的 [Azure 订阅](https://azure.microsoft.com/free)。

## <a name="provision-an-azure-storage-account"></a>预配 Azure 存储帐户

使用 Azure 存储的第一步是在 Azure 订阅中预配 Azure 存储帐户。

1. 如果你还没有完成此操作，请登录 [Azure 门户](https://portal.azure.com?azure-portal=true)。
1. On the Azure portal home page, select <bpt id="p1">**</bpt>&amp;#65291; Create a resource<ept id="p1">**</ept> from the upper left-hand corner and search for <bpt id="p2">*</bpt>Storage account<ept id="p2">*</ept>. Then in the resulting <bpt id="p1">**</bpt>Storage account<ept id="p1">**</ept> page, select <bpt id="p2">**</bpt>Create<ept id="p2">**</ept>.
1. 在“创建存储帐户”页上，输入以下值：
    - **订阅**：选择 Azure 订阅。
    - 资源组：使用所选名称创建新资源组。
    -               存储帐户名称：使用小写字母和数字输入存储帐户的唯一名称。
    - 区域：选择任何可用位置。
    -               性能：标准
    -               冗余：本地冗余存储 (LRS)

1. Select <bpt id="p1">**</bpt>Next: Advanced &gt;<ept id="p1">**</ept> and view the advanced configuration options. In particular, note that this is where you can enable hierarchical namespace to support Azure Data Lake Storage Gen2. Leave this option <bpt id="p1">**</bpt><bpt id="p2">&lt;u&gt;</bpt>unselected<ept id="p2">&lt;/u&gt;</ept><ept id="p1">**</ept> (you'll enable it later), and then select <bpt id="p3">**</bpt>Next: Networking &gt;<ept id="p3">**</ept> to view the networking options for your storage account.
1. Select <bpt id="p1">**</bpt>Next: Data protection &gt;<ept id="p1">**</ept> and then in the <bpt id="p2">**</bpt>Recovery<ept id="p2">**</ept> section, <bpt id="p3">&lt;u&gt;</bpt>de<ept id="p3">&lt;/u&gt;</ept>select all of the <bpt id="p4">**</bpt>Enable soft delete...<ept id="p4">**</ept> options. These options retain deleted files for subsequent recovery, but can cause issues later when you enable hierarchical namespace.
1. 继续转到其余的“下一步 >”页面，不更改任何默认设置，然后在“查看 + 创建”页上，等待你的选择通过验证，然后选择“创建”以创建 Azure 存储帐户。  
1. Wait for deployment to complete. Then go to the resource that was deployed.

## <a name="explore-blob-storage"></a>了解 Blob 存储

现在，你已有一个 Azure 存储帐户，可以为 blob 数据创建容器。

1. 从 `https://aka.ms/product1.json` 下载 [product1.json](https://aka.ms/product1.json?azure-portal=true) JSON 文件，并将它保存在你的计算机上（可以将它保存在任何文件夹中 - 稍后将它上传到 Blob 存储）。

                  如果浏览器中显示了 JSON 文件，请将该页另存为 product1.json。

1. 在存储容器的“Azure 门户”页左侧的“数据存储”部分中，选择“容器”。
1. 在“容器”页中，选择“&#65291; 容器”，然后添加一个名为 data 的新容器，其公共访问级别为“专用(不允许匿名访问)”   。
1. 创建“data”容器后，验证它是否在“容器”页中列出。
1. In the pane on the left side, in the top section, select **Storage browser **. This page provides a browser-based interface that you can use to work with the data in your storage account.
1. 在“存储浏览器”页中，选择“Blob 容器”，然后验证是否已列出“data”容器。
1. 选择“data”容器，注意它是空的。
1. 选择“&#65291; 添加目录”，阅读有关文件夹的信息，然后创建名为 products 的新目录 。
1. 在存储浏览器中，验证当前视图是否显示刚刚创建的“products”文件夹的内容，观察页面顶部的“痕迹导航”是否反映了路径“Blob 容器”>“data”>“products” 。
1. 在痕迹导航中，选择“data”以切换到“data”容器，注意它<u>不</u>包含名为“products”的文件夹。

    Folders in blob storage are virtual, and only exist as part of the path of a blob. Since the <bpt id="p1">**</bpt>products<ept id="p1">**</ept> folder contained no blobs, it isn't really there!

1. 使用“&#10514; 上传”按钮打开“上传 blob”面板。 
1. In the <bpt id="p1">**</bpt>Upload blob<ept id="p1">**</ept> panel, select the <bpt id="p2">**</bpt>product1.json<ept id="p2">**</ept> file you saved on your local computer previously. Then in the <bpt id="p1">**</bpt>Advanced<ept id="p1">**</ept> section, in the <bpt id="p2">**</bpt>Upload to folder<ept id="p2">**</ept> box, enter <bpt id="p3">**</bpt>product_data<ept id="p3">**</ept> and select the <bpt id="p4">**</bpt>Upload<ept id="p4">**</ept> button.
1. 如果“上传 blob”面板仍处于打开状态，请将其关闭，并验证是否已在“data”容器中创建 product_data 虚拟文件夹。
1. 选择 product_data 文件夹，并验证它是否包含已上传的 product1.json blob。
1. 在左侧的“数据存储”部分中，选择“容器”。
1. 打开“data”容器，并验证是否已列出你创建的 product_data 文件夹。
1. Select the <bpt id="p1">**</bpt>&amp;#x2027;&amp;#x2027;&amp;#x2027;<ept id="p1">**</ept> icon at the right-end of the folder, and note that it doesn't display any options. Folders in a flat namespace blob container are virtual, and can't be managed.
1. 使用“data”页右上角的“X”图标关闭页面并返回到“容器”页。

## <a name="explore-azure-data-lake-storage-gen2"></a>了解 Azure Data Lake Storage Gen2

Azure Data Lake Store Gen2 support enables you to use hierarchical folders to organize and manage access to blobs. It also enables you to use Azure blob storage to host distributed file systems for common big data analytics platforms.

1. 从 `https://aka.ms/product2.json` 下载 [product2.json](https://aka.ms/product2.json?azure-portal=true) JSON 文件，并将它保存在你的计算机上（之前下载 product1.json 的同一文件夹中 - 稍后将它上传到 Blob 存储）。
1. 在存储账户的“Azure 门户”页的左侧，向下滚动到“设置”部分，然后选择“Data Lake Gen2 升级” 。
1. In the ****Data Lake Gen2 upgrade**** page, expand and complete each step to upgrade your storage account to enable hierarchical namespace and support Azure Data Lake Storage Gen 2. This may take some time.
1. 升级完成后，在左侧窗格中的顶部，选择“存储浏览器”，然后导航回 data Blob 容器的根目录，其中仍包含 product_data 文件夹。  
1. 选择 product_data 文件夹，并确认它仍包含之前上传的 product1.json 文件。
1. 使用“&#10514; 上传”按钮打开“上传 blob”面板。 
1. 在 Azure 门户主页的左上角，选择“&#65291; 创建资源”，并搜索“存储帐户”。
1. 如果“上传 blob”面板仍处于打开状态，请将其关闭，并验证 product_data 文件夹现在是否包含 product2.json 文件。
1. 在左侧的“数据存储”部分中，选择“容器”。
1. 打开“data”容器，并验证是否已列出你创建的 product_data 文件夹。
1. 选择文件夹右端的 &#x2027;&#x2027;&#x2027; 图标，并注意在启用分层命名空间后，你可以在文件夹级别执行配置任务；包括重命名文件夹和设置权限。
1. 使用“data”页右上角的“X”图标关闭页面并返回到“容器”页。

## <a name="explore-azure-files"></a>了解 Azure 文件存储

Azure 文件存储为创建基于云的文件共享提供了一种方法。

1. 在存储容器的“Azure 门户”页左侧的“数据存储”部分中，选择“文件共享”。
1. 在“文件共享”页中，选择“&#65291; 文件共享”，并使用“事务优化”层添加名为 files 的新文件共享  。
1. 在“文件共享”中，打开新的“文件”共享。
1. 然后在出现的“存储帐户”页中，选择“创建”。
1. 关闭“连接”窗格，然后关闭“文件”页以返回到 Azure 存储帐户的“文件共享”页。

## <a name="explore-azure-tables"></a>了解 Azure 表

Azure 表为需要存储数据值但不需要关系数据库的完整功能和结构的应用程序提供了键/值存储。

1. 在存储容器的“Azure 门户”页左侧的“数据存储”部分中，选择“表”。
1. 在“表”页上，选择“&#65291; 表”并创建名为 products 的新表。  
1. 创建 products 表后，在左侧窗格的顶部，选择“存储浏览器” 。
1. 在存储资源管理器中，选择“表”并验证是否已列出“products”表。
1. 选择“products”表。
1. 在 products 页中，选择“&#65291;添加实体” 。
1. 在“添加实体”面板中，输入以下键值：
    -               PartitionKey：1
    -               RowKey：1
1. 选择“添加属性”，然后创建一个具有以下值的新属性：

    |属性名称 | 类型 | 值 |
    | ------------ | ---- | ----- |
    | 名称 | String | 小组件 |

1. 添加具有以下值的第二个属性：

    |属性名称 | 类型 | 值 |
    | ------------ | ---- | ----- |
    | 价格 | Double | 2.99 |

1. 选择“插入”，将新实体的行插入表中。
1. 在存储浏览器中，验证是否已向“products”表添加行，并且是否已创建“Timestamp”列来指示上次修改该行的时间。
1. 使用以下属性将另一个实体添加到“products”表中：

    |属性名称 | 类型 | 值 |
    | ------------ | ---- | ----- |
    | PartitionKey | 字符串 | 1 |
    | RowKey | 字符串 | 2 |
    | 名称 | String | Kniknak |
    | 价格 | Double | 1.99 |
    | 已中断 | 布尔 | 是 |

1. 插入新实体后，验证表中是否显示了包含已停用产品的行。

    You have manually entered data into the table using the storage browser interface. In a real scenario, application developers can use the Azure Storage Table API to build applications that read and write values to tables, making it a cost effective and scalable solution for NoSQL storage.

> 提示：如果已完成浏览 Azure 存储，则可以删除在本练习中创建的资源组。
