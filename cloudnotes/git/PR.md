在 GitHub 中，**PR 是 Pull Request（拉取请求）的缩写**。它是 GitHub 协同工作的核心功能，可以把它理解为一个 **「请求他人将你的代码合并进去」** 的操作。这不仅仅是一个简单的合并请求，更是一个**代码审查和团队协作的讨论平台**[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://worktile.com/kb/ask/536537.html)[](https://intersect-training.org/collaborative-git/pr.html)。

下面从几个方面为你详细介绍 PR：

### 1. PR 的核心概念：为什么需要它？

在一个多人协作的项目中，尤其是开源项目，通常只有核心维护者有权限直接修改主分支（如 `main` 或 `master`）。当一个贡献者（可能是陌生人）想为项目添加新功能或修复 Bug 时，他不能直接修改主代码库。

PR 机制就是为了解决这个问题而生的：

- **安全的贡献方式**：贡献者可以在自己的项目副本（Fork）中工作，完成后通过 PR 请求原项目拉取他的修改[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://worktile.com/kb/ask/536537.html)。
    
- **代码审查（Code Review）**：维护者和其他贡献者可以在 PR 页面查看每一行代码改动，并提出意见或建议。这能极大地保证代码质量[](https://worktile.com/kb/ask/536537.html)[](https://intersect-training.org/collaborative-git/pr.html)[](https://articles.mergify.com/pull-request-github/#/portal/signup)。
    
- **讨论与改进**：PR 提供了一个讨论区，大家可以在合并代码前充分交流。作者也可以根据反馈继续推送新的修改，PR 会自动更新[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://intersect-training.org/collaborative-git/pr.html)。
    

### 2. 典型的 PR 工作流程

一个标准的 PR 流程通常包含以下几个步骤，这也被称为 **GitHub Flow**[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)：

1. **派生（Fork）项目**：如果你没有目标项目的直接权限，首先需要在 GitHub 上点击 "Fork" 按钮，将项目复制一份到自己的账户下[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://worktile.com/kb/ask/536537.html)。
    
2. **克隆（Clone）到本地**：将 Fork 后的仓库（或你有权限的仓库）克隆到本地电脑上[](https://cloud.tencent.cn/developer/article/2324943?from=15425)[](https://worktile.com/kb/ask/536537.html)。
    
3. **创建新分支**：在本地创建一个新的分支（例如 `feature-add-login`）来进行你的修改。这能保持主分支的整洁[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://cloud.tencent.cn/developer/article/2324943?from=15425)。
    
4. **提交修改**：在新分支上完成代码编写和测试，然后进行提交（Commit）并推送到你的远程 GitHub 仓库[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://cloud.tencent.cn/developer/article/2324943?from=15425)。
    
5. **发起 PR**：在 GitHub 网站上，你会看到一个提示，点击 "Compare & pull request" 按钮。你需要填写一个清晰的标题和描述，说明你做了什么修改以及为什么这么做，然后点击 "Create pull request" 提交请求[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://cloud.tencent.cn/developer/article/2324943?from=15425)[](https://data.poverty-action.org/software/git/pull-request.html)。
    
6. **讨论与审查**：项目维护者和其他人会看到你的 PR，他们可以在代码的特定行留下评论，提出问题或改进建议[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://intersect-training.org/collaborative-git/pr.html)。
    
7. **持续修改**：根据审查意见，你可以在本地继续修改代码，并将新的提交推送到同一个分支。这些新的提交会自动添加到这个 PR 中，无需创建新的 PR[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://cloud.tencent.cn/developer/article/2324943?from=15425)[](https://intersect-training.org/collaborative-git/pr.html)。
    
8. **合并（Merge）PR**：当审查通过，且所有自动化测试都成功后，拥有权限的维护者就可以点击 "Merge pull request" 按钮，将你的修改合并到目标分支（如 `main`）中[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://intersect-training.org/collaborative-git/pr.html)。
    
9. **清理分支**：合并后，无论是远程还是本地的功能分支通常都可以安全地删除，以保持仓库整洁[](https://intersect-training.org/collaborative-git/pr.html)[](https://data.poverty-action.org/software/git/pull-request.html)。
    

### 3. PR 页面的主要构成

一个 PR 创建后，其页面通常包含以下几个关键标签页，方便协作[](https://intersect-training.org/collaborative-git/pr.html)：

- **Conversation（对话）**：这是 PR 的主页，可以看到所有评论、提交历史以及合并状态的更新。
    
- **Commits（提交）**：列出了这个 PR 中包含的所有代码提交，方便追溯每一步的修改。
    
- **Files Changed（文件改动）**：这里是代码审查的核心区域。可以清晰地看到这次 PR 增加了哪些代码（绿色），删除了哪些代码（红色）。审查者可以在这里针对具体某一行代码进行评论[](https://git-scm.com/book/zh/v2/GitHub-%E5%AF%B9%E9%A1%B9%E7%9B%AE%E5%81%9A%E5%87%BA%E8%B4%A1%E7%8C%AE?hmsr=joyk.com&utm_source=joyk.com&utm_medium=referral)[](https://intersect-training.org/collaborative-git/pr.html)。
    

### 总结

简单来说，GitHub 中的 **PR 就是一种「请求合并代码」的机制，它将代码修改、团队讨论和质量检查融合在一起，是现代软件开发协作中不可或缺的一环**。