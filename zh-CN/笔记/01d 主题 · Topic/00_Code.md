---
aliases: []
fileClass: evergreen-note
category-evergreen-note: topic
category-topic: develop
create: 2025-10-01 17:48:22
---
Related-Tag:: #运维
**Not processed Notes**
```dataviewjs
// 获取当前页面
let currentPage = this.current();
let currentPath = currentPage.file.path;
let currentLink = currentPage.file.link;

// 获取标签列表
let tags = currentPage.file.etags;

// 定义要排除的文件夹路径（确保以斜杠结尾）
const excludeFolders = [
    "04 丁 · Setting/",
    "01 甲 · Zettelkasten/01c 常青 · Evergreen/",
    "05 戊 · Project/"
];

let notesMap = {};

// 遍历所有标签
tags.forEach(tag => {
    // 构建查询字符串，排除当前页面本身
    let query = `${tag} and !"${currentPath}"`;

    dv.pages(query).forEach(note => {
        let path = note.file.path;
        let link = note.file.link;
        let inlinks = note.file.inlinks;

        // 排除特定文件夹下的笔记
        let isInExcludedFolder = excludeFolders.some(folder => path.startsWith(folder));

        if (!isInExcludedFolder &&
            !inlinks.includes(currentLink) && // 未链接到当前页面
            inlinks.length === 0 // 没有被任何笔记链接
        ) {
            notesMap[link] = link;
        }
    });
});

// 输出唯一笔记链接列表
dv.list(Object.values(notesMap));

```
# code
[[常用命令]]
[[代码随想录]]
