# auto-green
### 修改自<https://github.com/justjavac/auto-green>（已删库）[修改的地方](https://github.com/Geekertao/auto-green/blob/main/README.md#%E4%BF%AE%E6%94%B9%E7%9A%84%E5%9C%B0%E6%96%B9)

[![Build Status](https://github.com/Geekertao/auto-green/workflows/ci/badge.svg?branch=master)](https://github.com/Geekertao/auto-green/actions)

自动保持 GitHub 提交状态常绿。

> a commit a day keeps your girlfriend away.

## 原理

使用 GitHub Actions 的定时任务功能，每隔一段时间自动执行 `git commit`，提交信息为 "a commit a day keeps your girlfriend away"，灵感来自知乎问题[在 GitHub 上保持 365 天全绿是怎样一种体验？](https://www.zhihu.com/question/34043434/answer/57826281)下某用户的回答：

> 曾经保持了 200 多天全绿，但是冷落了女朋友，一直绿到现在。

有关 Github Action 的原理，可查看官方文档 [Github Action 简介](https://docs.github.com/cn/actions/learn-github-actions/introduction-to-github-actions)

## 使用

- 点右上角 **Use this template** 按钮复制本 GitHub 仓库，**:warning: 千万不要 Fork，因为 fork 项目的动态并不会让你变绿 :warning:**
- 修改 [ci.yml 文件的第 63、64 行](./.github/workflows/ci.yml#L63-L64) 为自己的 GitHub 账号和昵称
- (可选) 你可以通过修改 [ci.yml 文件的第 81、82 行](./.github/workflows/ci.yml#L77-L78)来调整提交日频率（第70行name也可修改，便于辨别其操作）
- （可选）少提交日也可修改，同上，不提交日修改见[ci.yml](./.github/workflows/ci.yml)的注释。


> git remote set-url origin https://${{ github.actor }}:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }}

这里就是指定远程仓库等地址，这里有几个占位符，github 的 actor 和 repository 对象，其实这些我们不用管，在运行的时候会被自动赋值为当前仓库的信息，另外还有 GITHUB_TOKEN 也是在该任务运行的时候自动添加的。
**(重要)（额外操作）需要在仓库设置-Actions-General-Workflow permissions改为Read and write permissions**

> git commit --allow-empty -m "a commit a day keeps your girlfriend away"

这里的 commit 操作加上了一个 --allow-empty 选项，意思就是允许空的提交，这也就解释了上文空提交的缘由了。

## 修改的地方
将工作流重构为提交日5次提交，少提交日2次提交，每月随机3天不提交（都可修改）

## License

[auto-green](https://github.com/Geekertao/auto-green) is released under the MIT License. See the bundled [LICENSE](./LICENSE) file for details.
