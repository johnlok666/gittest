# CODEBUDDY.md

本仓库是个人知识与规范文档仓库，主要用于沉淀数据领域笔记与团队规范。

## 项目结构

| 路径 | 说明 |
| ---- | ---- |
| `index.md` | Flink 实时计算笔记提纲 |
| `OneData数据仓库建模规范.md` | OneData 数据仓库建模规范（权威定义，建模时以此为准） |
| `.gitignore` | 已排除嵌套仓库 `llvm-project/`（2.6GB，独立仓库，勿纳入跟踪） |
| `llvm-project/` | LLVM 源码克隆，独立 git 仓库，只读参考，不提交 |

## 环境与常用命令

- Git 可执行文件路径：`D:\opt\Git\cmd\git.exe`
- **Git 必须走代理**：全局已配置 `http.proxy` / `https.proxy` = `http://127.0.0.1:7897`。若代理客户端未运行，推送会 21 秒超时失败，此时需确认代理端口或临时 `--unset`
- Git 账号：`john <30907593@qq.com>`，远程 `origin` = `https://github.com/johnlok666/gittest.git`
- 本仓库无构建、无测试、无依赖安装步骤

## Git 工作流规范

1. **分支**：`main` 为唯一主分支。新功能分支统一用 `feature/<英文名>` 命名，不再使用历史遗留的错误拼写 `featrue`
2. **同步优先**：任何合并/推送前先 `git fetch origin`，确认本地不落后
3. **合并流程**：
   ```
   git fetch origin
   git switch feature/xxx
   git rebase origin/main       # 在自己的分支上解决冲突
   git push --force-with-lease origin feature/xxx
   # 最后在 GitHub 开 PR 合并到 main
   ```
4. **禁止**：`git push --force` 到 `main`；禁止在 `main` 上直接改写历史
5. **提交信息**：采用 Conventional Commits，一行中文描述
   - `docs:` 文档新增/修改
   - `chore:` 配置、`.gitignore` 等
   - `feat:` / `fix:` / `refactor:` 代码类变更
   - 示例：`docs: 新增 OneData 数据仓库建模规范`
6. **行尾**：提交统一为 LF（全局已设 `core.autocrlf=input`），Windows 本地编辑会出现 CRLF→LF 提示，属正常现象

## 文档撰写规范

- 编码 UTF-8，Markdown 格式
- 中文与英文/数字之间加空格；使用中文标点
- 规范类文档优先用表格呈现条目，配可复制的模板
- 新建规范文档时，若涉及数仓建模、指标体系、命名约定，**必须与 `OneData数据仓库建模规范.md` 保持一致**，冲突时以该文档为准

## 给 AI 助手的行为约定

- 每次涉及数仓建模/指标定义的需求，先阅读 `OneData数据仓库建模规范.md` 再动手
- 不要主动创建 `.md` 文档，除非用户明确要求
- 不要把 `llvm-project/` 内容加入本仓库提交
- 执行破坏性操作（强推、删除分支、改写历史）前先向用户确认
- 回复使用简体中文，简洁直接
