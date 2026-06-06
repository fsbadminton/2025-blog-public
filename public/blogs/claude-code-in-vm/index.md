

## 1.环境

- 宿主机：Windows

- 虚拟机：Ubuntu 22.04

- 网络模式：NAT

![](/blogs/claude-code-in-vm/75ab77d8651af25c.png)
## 2.网络配置

- 宿主机上通过`ipconfig`获取WLAN下的ip地址

- 虚拟机上配置代理环境变量，打开终端输入：

  ```bash
  export http_proxy=http://宿主机ip:代理端口
  export https_proxy=http://宿主机ip:代理端口
  ```

- 写入永久配置：

  ```bash
  echo 'export http_proxy=http://宿主机ip:代理端口' >> ~/.bashrc
  echo 'export https_proxy=http://宿主机ip:代理端口' >> ~/.bashrc
  source ~/.bashrc
  ```

> **注意：** 请将 `宿主机ip` 替换为实际的宿主机 IP 地址，`代理端口` 替换为实际的代理端口号（如 `7890`）。

## 3.安装ClaudeCode CLI

- 执行以下命令，等待安装完成

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

- 验证安装

  ```bash
  which claude
  ```

- 也可以通过以下方式确认：

  ```bash
  ls ~/.local/bin
  ```

- 如果看到：

  ```bash
  claude
  ```

  说明已经装好，只是 **PATH** 没有配置

## 4.把Claude加入PATH

- 编辑 `.bashrc`：

```bash
nano ~/.bashrc
```

- 在最后加一行：

```bash
export PATH="$HOME/.local/bin:$PATH"
```

- 保存退出

- `Ctrl + O` → 回车→`Ctrl + X`

- 让它生效

```bash
source ~/.bashrc
```

- 验证

```bash
claude --help
```

如果能输出帮助信息，说明：

👉 ✅ 成功加入环境变量

## 5.安装CC-Switch (CCS)

- 检查系统架构

  ```bash
  uname -m
  ```

- 打开浏览器，在 GitHub 上搜索 `cc-switch` 进行版本下载（以下以 v3.16.1 为例，实际以下载版本为准）

  ![](/blogs/claude-code-in-vm/459d05171a1c6978.png)

- 下载后安装（注意选择与系统架构匹配的安装包）

  ```bash
  cd ~/Downloads
  sudo apt install ./CC-Switch-v3.16.1-Linux-x86_64.deb
  ```

## 6.配置API Key

- 打开CCS，选择ClaudeCLI标志，点击右边 ➕ 进行配置

 ![](/blogs/claude-code-in-vm/a4dc6f0fae900d29.png)

- 选择**自定义配置**，填入API Key和请求地址，在高级选项获取模型列表进行模型设置后添加即可

![](/blogs/claude-code-in-vm/0164a1b7b97a1259.png)

## 7.使用

配置完成后，在CCS中选择一个`workspace`（即你想要Claude Code工作的项目目录），然后在终端中进入该目录，执行：

```bash
claude
```

即可启动Claude Code。