---
title: 记一次 Pearson 电子书导出破解
date: 2023-08-06 11:15:41
license: all_rights_reserved
abbrlink: 1015678645
---

前几天，打算把我那本 Pearson 的 Mathematics in Actions 的电子版发一本给我朋友。

没想到，找了半天硬是一个电子版都没有，连 扫描版 / 付费版 的都没。

于是，没办法，自己激活了官方的电子版，打算把账号密码直接发给别人。结果：

![](images/pearson_pic1.png)

Pearson 的垃圾电子书阅读器根本就不知道怎么翻页，甚至每一页只能看到中间部分，头尾看不到。

破解开始！

打开要下载的对应单元的第一页，

![](images/pearson_pic2.png)

先在检查元素里找图片链接，右键，新建标签页打开（不要直接复制链接，因为图片在iframe里，要打开图片链接后再复制），复制链接，链接是这样的：

`https://ebook4.ilongman.com/sbo/***/***/OEBPS/images/p01.jpg`

按照这个规律，打开`https://ebook4.ilongman.com/sbo/***/***/OEBPS/images/p01.jpg`，成功获取到了第二页的课本页面！

此时发现，课本的获取非常简单，只要在这个把最后的 `p01.jpg`替换相应页码就可以获取到高清jpg格式的完整课本页面。

按照此规律，写了一个脚本：

```python
import os
import requests

def download_images():
    base_url = "" #替换为去掉p01.jpg的url，格式为 https://ebook4.ilongman.com/sbo/***/***/OEBPS/images/
    save_dir = "" #替换为单元名称
    pagenum = 

    if not os.path.exists(save_dir):
        os.makedirs(save_dir)

    for page in range(1, pagenum):
        page_str = f"{page:02d}"
        image_url = f"{base_url}p{page_str}.jpg"
        response = requests.get(image_url)

        if response.status_code == 200:
            image_path = os.path.join(save_dir, f"p{page_str}.jpg")
            with open(image_path, "wb") as f:
                f.write(response.content)
            print(f"Page {page_str} downloaded successfully.")
        else:
            print(f"Failed to download page {page_str}.")

if __name__ == "__main__":
    download_images()

```

只需替换 base_url 为 `https://ebook4.ilongman.com/sbo/***/***/OEBPS/images/`这样的格式（链接后面的`/`一定要保留），save_dir
为单元名称，pagenum 为这一单元的总页码数量就可以下载一整个单元的课本页面。

重复以上步骤直到下载完所有单元的课本页面，然后就可以拼接 pdf 了。

打开 Adobe Acrobat DC，选择 创建PDF，再选择 多个文件，合并文件，下一步

![](images/pearson_pic3.png)

选择添加文件，然后把图片按单元顺序依次全选拖入 Adobe Acrobat DC 中。

最后，选择 合并 即可生成 PDF 文件。

![](images/pearson_pic4.png)

Enjoy~

