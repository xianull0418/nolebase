---
aliases: []
fileClass: evergreen-note
category-evergreen-note: topic
category-topic: research
create: 2025-09-26 19:59:39
---
Related-Tag:: #agent
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
# Agent
[[Agent.excalidraw]]
[[2025-09-11 BUPT-WangLab-林老师会议分享]]
![[00_Agent_image_1.png]]
AI Agent（智能体）相继成为各大科技巨头布局的新风口。比如微软推出了 AutoGen、谷歌 Deepmind 推出了 Robotic Agent、亚马逊推出了 Bedrock Agents、阿里云 ModelScopeGPT、斯坦福与谷歌联合搭建的名为《Smallville》的虚拟小镇等等
 [[Agent_planning]]

## Agent survey
[[A Survey on Large Language Model based Autonomous Agents]]
[[The Rise and Potential of Large Language Model Based Agents - A Survey]]
[[The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling - A Survey]]

## 生信 Agent