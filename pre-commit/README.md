git hook 被放置在 `.git/hooks`目录下。由于`.git`文件夹是不会被 git 跟踪的，所以`.git/hooks`目录下的 hooks 钩子无法提交到代码仓库，就不能和他人共享钩子脚本。为了解决 git hook 共享的问题，可以使用 pre-commit 工具。pre-commit 工具的思路是通过 .pre-commit-config.yaml 文件来维护 git hook 钩子，并通过脚本在 .git/hooks`目录下生成相应的 git hook。这也是每次修改 .pre-commit-config.yaml，需要执行 pre-commit install 的原因。而且该文件可以提交到代码仓库。多个开发者可以通过同一个 .pre-commit-config.yaml 共享 git hook。

#### 1.1.1. 本地安装 pre-commit，则 follow 以下步骤

该工具的使用可以遵循以下步骤：

1. 安装 pre-commit

```bash
brew install pre-commit
```

2. check 是否安装成功

```bash
pre-commit --version
```

如果正常输出 pre-commit 版本号，则说明安装成功。

3.添加 pre-commit 配置文件

- 在项目根目录创建 `.pre-commit-config.yaml`

  ```bash
  touch .pre-commit-config.yaml
  ```
- 在 .pre-commit-config.yaml 文件配置需要执行的 hook
  示例：

  ```yaml
  repos:
    - repo: https://github.com/ejba/pre-commit-maven
      rev: v0.3.3
      hooks:
        - id: maven
          args: [ 'clean compile' ]
        - id: maven-checkstyle
    - repo: https://github.com/dustinsand/pre-commit-jvm
      rev: v0.6.0
      hooks:
        - id: pmd
  ```

  .pre-commit-config.yaml 具体的写法，参考 [pre-commit](https://pre-commit.com)。有那些可以使用的 hook，可以参考 [pre-commit hook](https://pre-commit.com/hooks.html)。

4. 安装 git hook 脚本

```bash
$ pre-commit install
pre-commit installed at .git/hooks/pre-commit
```

执行这个命令，将使 .pre-commit-config.yaml 中定义的 hooks 生效。

通过以上 4 个步骤，当我们执行 commit 之前，会自动执行我们的 git hooks。
