# Ubuntu Good Practice

<img height="55" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/ubuntu/ubuntu-original-wordmark.svg" />

The best configurations and practices on my Ubuntu Linux to record!

## Gnome Teak

UI 魔改神器

```bash
sudo apt-get update
sudo apt-get install gnome-tweak-tool
```

## Font Better

Ubuntu，准确说所有 Linux 的 UI 下的字体都很烂，我们搞点好看的。

第一，扩展 Nerd 字体

```bash
git clone https://github.com/devilyouwei/linux-font.git

mkdir ~/.fonts

cp -rf ./linux-font/* ~/.fonts/
```
