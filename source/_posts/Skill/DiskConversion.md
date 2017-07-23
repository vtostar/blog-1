---
title: 硬盘分区转换命令
date: 2016-03-11
categories: Skill
tags:
  - computer
---

1. 在系统安装界面按 `Shift+F10` 打开命令提示符（如果不行就试试 `Fn+Shift+F10`）
2. 输入：`diskpart`
3. 输入：`list disk`，展示所有磁盘信息
4. 输入：`select disk 0`，0 是指选择第 0 号磁盘。如果你有一块以上的磁盘，则需要根据磁盘容量判断应当选择的磁盘
5. 输入：`clean`，清空当前磁盘所有数据
6. 若输入：`convert mbr`，则转换为 mbr 分区；若输入：`convert gpt`，则转换为 gpt 分区。
