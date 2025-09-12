# Inno Setup Chinese Simplified Translation #
Inno Setup 简体中文翻译

[![GitHub issues](https://img.shields.io/github/issues/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/issues)
[![GitHub forks](https://img.shields.io/github/forks/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/network)
[![GitHub stars](https://img.shields.io/github/stars/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/stargazers)
[![GitHub license](https://img.shields.io/github/license/kira-96/Inno-Setup-Chinese-Simplified-Translation)](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation)

**注意：此翻译版本支持 Inno Setup 6.5.0+ 的软件，Inno Setup 5 的翻译文件在[这里](https://github.com/kira-96/Inno-Setup-Chinese-Simplified-Translation/tree/5.5.3+)**

## 食用方法 ##

### 本地环境 ###

- **Step 1**

  将**ChineseSimplified.isl**放到**Inno Setup安装目录**下的"Languages"文件夹里面

- **Step 2**

  如果你是通过新建脚本的方式创建脚本，在**Languages**选项勾选**Chinese Simplified**即可：

  ![wizard](Wizard.png)

  如果你需要在现有脚本中添加简体中文支持，直接在你的脚本的`[Languages]`部分添加下面一行即可：

  ``` iss
  Name: "chinesesimplified"; MessagesFile: "compiler:Languages\ChineseSimplified.isl"
  ```

  示例：

  ``` iss
  [Languages]
  Name: "english"; MessagesFile: "compiler:Default.isl"
  Name: "chinesesimplified"; MessagesFile: "compiler:Languages\ChineseSimplified.isl"
  ```

### 持续集成（CI）环境 ###

- **Step 1**

  将**ChineseSimplified.isl**放到你的项目仓库里面

- **Step 2**

  与本地操作类似，需要向现有脚本的`[Languages]`部分添加简体中文。其中`MessagesFile`参数为相对路径，即**ChineseSimplified.isl**相对该脚本的路径。示例：

  ``` iss
  [Languages]
  Name: "chinesesimplified"; MessagesFile: ".\ChineseSimplified.isl"
  ```

- **Step 3**

  安装与**ChineseSimplified.isl**版本相符的 Inno Setup

- **Step 4**

  执行打包作业

<details open>
<summary>示例：GitHub Actions 配置</summary>

考虑如下项目结构：

```
/
├── .github/
│   └── workflows/
│           example.yml
├── myfolder/
│       ChineseSimplified.isl
│       InnoSetup.iss
└── 其他文件
```

``` yaml
# .github/workflows/example.yml

name: Build and Package

on:
  push:

jobs:
  build:
    runs-on: windows-2022

    steps:
      - name: Checkout
        uses: actions/checkout@v5
      
      # 安装特定版本的 Inno Setup 并添加到环境变量
      - name: Install Inno Setup
        run: |
          # 发现异常时报错
          $ErrorActionPreference = 'Stop'
          $PSNativeCommandUseErrorActionPreference = $true

          curl.exe -OL https://files.jrsoftware.org/is/6/innosetup-6.5.0.exe
          .\innosetup-6.5.0.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART
          "C:\Program Files (x86)\Inno Setup 6" >> $env:GITHUB_PATH
        shell: pwsh
        
      # 中间的步骤是编译你自己项目产物，这里省略
        
      # 执行 Inno Setup 打包
      - name: Build Installer
        run: ISCC.exe myfolder\InnoSetup.iss
        shell: pwsh
```

</details>

### 链接 ###

- [Inno Setup](https://jrsoftware.org/isinfo.php)
- [issrc](https://github.com/jrsoftware/issrc)
