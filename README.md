# Inno Setup Chinese Simplified Translation #
Inno Setup 简体中文翻译

[![GitHub issues](https://img.shields.io/github/issues/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/issues)
[![GitHub forks](https://img.shields.io/github/forks/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/network)
[![GitHub stars](https://img.shields.io/github/stars/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/stargazers)
[![GitHub license](https://img.shields.io/github/license/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation)

## 本地食用方法 ##

- **Step 1**

  将**ChineseSimplified.isl**放到**Inno Setup安装目录**下的"Languages"文件夹里面

- **Step 2**

  如果你是通过新建脚本的方式创建脚本，在**Languages**选项勾选**Chinese Simplified**即可：

  ![wizard](Wizard.png)

  如果你需要在现有脚本中添加简体中文支持
  直接在你的脚本的`[Languages]`部分添加下面一行即可

  ``` yaml
  Name: "chinesesimplified"; MessagesFile: "compiler:Languages\ChineseSimplified.isl"
  ```

  示例：

  ``` yaml
  [Languages]
  Name: "english"; MessagesFile: "compiler:Default.isl"
  Name: "chinesesimplified"; MessagesFile: "compiler:Languages\ChineseSimplified.isl"
  ```

## GitHub Actions 食用方法 ##

- **Step 1**

  将**ChineseSimplified.isl**放在你的项目仓库中

- **Step 2**

  将你项目的 iss 脚本的语言设置为`chinesesimplified`，并指定语言文件的路径
  > 此处的路径是语言文件在你项目的相对路径
  ```iss
  [Languages]
  Name: "chinesesimplified"; MessagesFile: ".\myfolder\ChineseSimplified.isl"
  ```
- **Step 3**

  配置工作流安装**指定版本**的 Inno Setup

- **Step 4**

  执行打包作业

### Workflow 配置示例

以下是一个 GitHub Actions 工作流示例

```
# 项目结构示例
├── .github/
│   └── workflows/
│           example.yml
├── myfolder/
│       ChineseSimplified.isl
│       InnoSetup.iss
└── 其他文件
```

```yml
name: Build and Release

on:
  push:
    tags:
      - "v*"

jobs:
  build:
    runs-on: windows-2022

    steps:
      - name: Checkout
        uses: actions/checkout@v3
      
      # 安装指定版本的 Inno Setup，并添加到环境变量
      - name: Install Inno Setup
        run: |
          curl -OL https://files.jrsoftware.org/is/6/innosetup-6.5.0.exe
          .\innosetup-6.5.0.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART
          "C:\Program Files (x86)\Inno Setup 6" >> $env:GITHUB_PATH
        shell: pwsh
        
      # 中间的步骤是编译你自己项目产物，这里进行省略
        
      # 执行Inno Setup打包  
      - name: Build Installer
        run: |
          cd myfolder
          ISCC.exe InnoSetup.iss
        shell: pwsh
```


**注意：此翻译版本支持 Inno Setup 6.5.0+ 的软件，Inno Setup 5 的翻译文件在[这里](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/tree/5.5.3+)**

### 链接 ###

- [Inno Setup](https://jrsoftware.org/isinfo.php)
- [issrc](https://github.com/jrsoftware/issrc)
