很多 Ubuntu 桌面用户常会遇到的问题！字体有模糊/锯齿/颗粒感，通常与**字体渲染设置**、**屏幕缩放**、**缺省字体本身品质**以
及**缺少合适现代字体**有关。下面为你详细讲解优化方案，并给出跨语言友好的字体推荐和安装方式。

---

## 一、**渲染优化：字体模糊主要原因及设置**

### 1. 检查显示设置

-   **显示器缩放**（scale factor）如果不是 1 倍整数、或分辨率没最佳，会影响 UI 清晰度。
-   GNOME 下：  
    `设置 → 显示器`，确认缩放系数、分辨率与显示器物理分辨率一致。

### 2. 字体平滑和 Hinting

-   进入 `设置 → 外观 → 字体` 或 `gnome-tweaks（Tweaks）→ 字体`。
-   `字体抗锯齿` 选项选择“Subpixel（子像素）”，
-   `Hinting` 选项选择“中等（Medium）”或“完美（Slight/Full）”，实际体验下哪个锐利。

_如未装“优化工具”，先安装命令：_

```bash
sudo apt install gnome-tweaks
```

然后运行 `gnome-tweaks`。

---

## 二、**推荐更好看的现代字体并全局替换**

### 1. 英文字体推荐

-   **Noto Sans / Noto Sans Mono**（Google，支持多语种全球覆盖）
-   **Fira Sans / Fira Mono**（极适合 UI 和代码）
-   **JetBrains Mono**（代码编辑器、终端极佳）
-   **Source Sans Pro / Source Code Pro**（Adobe 开源系列）
-   **Ubuntu / Ubuntu Mono**（Ubuntu 自带，但可用新版更协调）

### 2. 中文字体推荐

-   **Noto Sans CJK SC**（Google，Noto 字体亚洲多文种支持，包括简体、繁体、日文、韩文）
-   **思源黑体/思源宋体**（Source Han Sans / Source Han Serif，Adobe/Google 开源，与 Noto 是同一底层设计）
-   **霞鹜文楷（LXGW WenKai）**：优秀中文显示/代码字体，可搭配西文字体
-   **文泉驿微米黑**（WenQuanYi Micro Hei，老牌开源方案）

### 3. 其它语言字体

Noto family 几乎覆盖全球所有语种（阿拉伯、越南、印度诸语言等），Code/Mono/Serif/Sans 完整！

---

## 三、**字体安装方法和全局设置**

### 1. 安装推荐字体

```bash
# Google Noto（包含各国语言）
sudo apt install fonts-noto fonts-noto-cjk fonts-noto-mono

# 思源黑体/宋体
sudo apt install fonts-source-han-sans-cn fonts-source-han-serif-cn

# Ubuntu 字体
sudo apt install fonts-ubuntu

# JetBrains Mono
sudo apt install fonts-jetbrains-mono

# Fira 字体
sudo apt install fonts-firacode fonts-fira-mono fonts-fira-sans

# 文泉驿微米黑
sudo apt install fonts-wqy-microhei

# LXGW WenKai（需手动，见下）
```

#### **LXGW WenKai** （现代中英高质量字体，中文极佳）

1. 官方[下载页面](https://github.com/lxgw/LxgwWenKai/releases)下载安装包（`.ttf`）
2. 安装方法（假设在`~/Downloads`）：
    ```bash
    mkdir -p ~/.local/share/fonts
    cp ~/Downloads/LXGWWenKai*.ttf ~/.local/share/fonts/
    fc-cache -f -v  # 刷新缓存
    ```

---

### 2. 全局字体设置

#### GNOME 桌面环境下

1. 运行 `gnome-tweaks`（或“优化工具”）。
2. 设置：
    - **界面字体**（例如 `Noto Sans` / `Ubuntu`）
    - **文档字体** （同上，或常选 `Noto Sans`）
    - **等宽字体**（推荐 `Noto Sans Mono`/`Fira Mono`/`JetBrains Mono`/`Ubuntu Mono`）
    - **标题栏字体**（选你喜欢者，通常跟 UI 主字体一致即可）
3. 设置“抗锯齿”、“Hinting”为最佳观感。

#### KDE/Plasma

进入 `系统设置 → 外观 → 字体` 配置上述字体。

---

### 3. 字体优先级（多语言支持）的写法

以 `~/.config/fontconfig/fonts.conf` 为例，你可自定义优先级。例如（中西文混排友好技巧）：

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Noto Sans</family>
      <family>Noto Sans CJK SC</family>
      <family>LXGW WenKai</family>
      <family>WenQuanYi Micro Hei</family>
      <family>Ubuntu</family>
    </prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer>
      <family>Noto Sans Mono</family>
      <family>JetBrains Mono</family>
      <family>Fira Mono</family>
      <family>Ubuntu Mono</family>
      <family>Noto Sans Mono CJK SC</family>
      <family>LXGW WenKai Mono</family>
      <family>WenQuanYi Micro Hei Mono</family>
    </prefer>
  </alias>
</fontconfig>
```

改完可 `fc-cache -f -v` 刷新缓存。

---

### 4. 浏览器/编辑器字体

-   VSCode/Terminal 也可用上述字体，直接在设置中用 `"Noto Sans Mono, JetBrains Mono, Fira Mono, ..."`, 具体见前一回答。
-   浏览器可以在“首选字体”设置里选 `Noto Sans`,`思源黑体` 或 `LXGW WenKai`。

---

## 四、Ibus/Fcitx 输入法候选框字体模糊

有些输入法候选词字体也会异常，常见于 HiDPI/缩放，请通过：

-   Fcitx5: `配置工具→外观→主题→自定义字体` 显式选高分字体
-   IBus: 不支持可配置字体，但可尝试优化主桌面字体

---

## 五、终端字体清晰度优化（推荐新一代开源字体）

-   JetBrains Mono, Fira Code, Cascadia Code, Sarasa Gothic（更适合中英混合）

---

## 总结一句话

> 标配推荐：**Noto Sans**（西文/多语）、**Noto Sans CJK SC**（中文）+**JetBrains Mono**（代码）+**LXGW WenKai**（美观中
> 文），搭配上适合屏幕的抗锯齿设置，Ubuntu UI 体验可立刻提升至一线水准！
