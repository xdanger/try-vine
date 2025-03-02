# 开发环境设置

要开始使用 Vine 编程语言，您需要设置适当的开发环境。本章将指导您完成 Vine 开发工具的安装和配置过程。

## 系统要求

Vine 编译器可以在以下操作系统上运行：

- Linux（推荐 Ubuntu 20.04+）
- macOS（10.15 Catalina 或更新版本）
- Windows 10/11（通过 WSL 或本地安装）

最低硬件要求：

- 至少 4GB RAM
- 1GB 可用磁盘空间
- 64 位处理器

## 安装 Vine 编译器

### 方法 1：使用官方安装脚本（推荐）

这是最简单的安装方法，适用于大多数用户：

```bash
# 下载并运行安装脚本
curl -sSL https://vine.dev/install.sh | bash

# 或者使用 wget
# wget -qO- https://vine.dev/install.sh | bash
```

安装脚本会自动处理依赖关系，并将 Vine 编译器添加到您的路径中。

### 方法 2：从源代码构建

如果您想要最新的开发版本，或者希望自定义编译过程，可以从源代码构建：

```bash
# 克隆 Vine 仓库
git clone https://github.com/vine-lang/vine.git
cd vine

# 构建编译器
cargo build --release

# 将编译好的二进制文件添加到路径
export PATH="$PATH:$(pwd)/target/release"
```

注意：从源代码构建需要安装 Rust 工具链（版本 1.56 或更高）。

### 方法 3：使用 Docker 容器

如果您喜欢使用容器或者不想在本地系统上安装，可以使用 Docker：

```bash
# 拉取 Vine 官方 Docker 镜像
docker pull vinelang/vine:latest

# 运行容器并挂载当前目录
docker run -it --rm -v $(pwd):/workspace vinelang/vine:latest
```

## 验证安装

安装完成后，验证 Vine 编译器是否正确安装：

```bash
vine --version
```

您应该看到类似于以下内容的输出：

```
Vine v0.1.0 (experimental)
```

## 设置编辑器

为了获得最佳的开发体验，您可以配置代码编辑器以支持 Vine 语言。

### Visual Studio Code

1. 安装 VS Code（如果尚未安装）：从 [code.visualstudio.com](https://code.visualstudio.com/) 下载并安装

2. 安装 Vine 扩展：
   - 打开 VS Code
   - 转到扩展视图（Ctrl+Shift+X 或 Cmd+Shift+X）
   - 搜索 "Vine Language"
   - 点击安装

3. 配置 VS Code 设置（可选）：

   ```json
   {
     "vine.formatOnSave": true,
     "vine.lintOnSave": true,
     "editor.tabSize": 2
   }
   ```

### Vim/Neovim

1. 使用插件管理器（如 vim-plug）安装 Vine 语法高亮：

   ```vim
   " 在您的 .vimrc 或 init.vim 中添加
   Plug 'vine-lang/vim-vine'
   ```

2. 安装并配置插件：

   ```
   :source %
   :PlugInstall
   ```

### 其他编辑器

对于其他编辑器（如 Sublime Text、Atom、Emacs 等），可能尚未有官方支持。您可以：

- 使用通用的文本编辑功能
- 查看编辑器的扩展市场，看是否有社区贡献的 Vine 支持
- 临时配置使用类似语言的语法高亮（如 JavaScript 或 Rust）

## 创建项目目录结构

Vine 项目通常遵循以下目录结构：

```
my-vine-project/
├── src/
│   ├── main.vi       # 主程序入口
│   ├── lib.vi        # 库代码
│   └── ...           # 其他源文件
├── examples/         # 示例代码
├── tests/            # 测试文件
└── README.md         # 项目文档
```

您可以使用以下命令创建新项目：

```bash
# 创建项目目录
mkdir my-vine-project
cd my-vine-project

# 创建基本目录结构
mkdir -p src examples tests

# 创建主文件
touch src/main.vi
```

## 配置文件（可选）

在项目根目录中，您可以创建 `vine.toml` 配置文件来自定义编译选项和项目设置：

```toml
[project]
name = "my-vine-project"
version = "0.1.0"
authors = ["Your Name <your.email@example.com>"]

[build]
target = "main"
optimization = "debug"  # 或 "release"

[dependencies]
# 未来可能支持的依赖声明
```

## 故障排除

如果您在安装或设置过程中遇到问题，请尝试以下解决方案：

### 常见问题

1. **命令未找到错误**:

   ```
   command not found: vine
   ```

   解决方案：确保 Vine 已添加到您的 PATH 中：

   ```bash
   echo 'export PATH="$PATH:$HOME/.vine/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

2. **权限错误**:

   ```
   Permission denied
   ```

   解决方案：使用 sudo 或修复目录权限：

   ```bash
   sudo chmod +x $HOME/.vine/bin/vine
   ```

3. **依赖缺失**:

   ```
   Missing dependency: ...
   ```

   解决方案：安装必要的系统包：

   ```bash
   # Ubuntu/Debian
   sudo apt-get update && sudo apt-get install build-essential

   # macOS
   xcode-select --install

   # Windows
   # 安装 Visual Studio Build Tools
   ```

## 下一步

完成环境设置后，您可以继续学习创建您的[第一个 Vine 程序](./03-first-program.md)。

在下一章中，我们将创建一个简单的 "Hello, World!" 程序，探索基本的 Vine 语法，并学习如何编译和运行 Vine 代码。
