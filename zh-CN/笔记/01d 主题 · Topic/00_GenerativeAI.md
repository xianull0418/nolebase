---
aliases: []
fileClass: evergreen-note
category-evergreen-note: topic
category-topic:
create: 2025-10-05 15:32:53
---
Related-Tag:: #generativeAI #大模型 #NLP 
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
# 00_GenerativeAI
## 论文
[[公开模型一切，优于DeepSeek-R1，英伟达开源Llama-Nemotron家族]]
[[LANGUAGE AGENTS MEET CAUSALITY – BRIDGING LLMS AND CAUSAL WORLD MODELS]]
## 传统 NLP 概念
[[词袋特征]]
[[N-gram]]
[[NLP-Beginner 任务一：基于机器学习的文本分类]]
## 参数相关
[[大模型的参数量]]
## 概念相关
[[语义空间]]
[[大语言模型常用微调框架介绍]]
[[Alpaca 格式]]
[[ShareGPT 格式]]
[[Scaling Law]]
[[MCP]]
[[LlamaFactory]]
[[多模态 AI 核心技术：CLIP 与 SigLIP 技术原理与应用进展]]
[[长尾问题]]
[[异方差不确定性]]
[[认知不确定性]]
[[Reward Model]]
[[因果推断]]
[[反事实一致性]]
[[RLHF]]
[[世界偏好模型]]
[[大模型输出的过程]]
[[嵌入模型的池化]]
[[嵌入模型原理]]
[[上下文自适应嵌入]]

## 训练相关
[[Zero-shot]]
[[Few-shot]]
[[COT]]

## 扩散模型
[[条件扩散模型：Classifier-Guidance]]
[[扩散模型]]
[[扩散模型与图像生成]]
[[自编码器]]
[[自编码器和扩散模型]]
[[扩散模型的训练过程]]
## 嵌入问题
[[一词多义]]