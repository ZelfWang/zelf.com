# Zelf.com 双版本部署说明

本压缩包包含两个独立版本：

- `index.html`：电脑端
- `mobile.html`：移动端
- `style.css`：电脑端样式
- `mobile.css`：移动端样式
- `CNAME`：自定义域名
- `README_CN.md`：说明

## 自动判断电脑还是手机

`index.html` 顶部包含自动判断脚本。

它同时检查：

1. 浏览器 User-Agent 是否包含 Android / iPhone / Mobile
2. 浏览器宽度是否小于 768px

如果满足其中之一，就自动跳转：

```text
mobile.html
```

因此用户正常打开：

```text
https://zelf.com
```

电脑会留在桌面版，手机会自动进入移动版。

`mobile.html` 也有反向判断：
如果用很宽的电脑屏幕直接打开 `mobile.html`，会自动回到桌面版。

## 强制访问某个版本

为了测试，我加入了参数：

电脑强制打开桌面版：

```text
https://zelf.com/index.html?desktop=1
```

手机强制打开移动版：

```text
https://zelf.com/mobile.html?mobile=1
```

## 更推荐的技术方式

实际上，从 SEO、维护成本和兼容性来说，最佳实践通常是：

```text
一个网址 + Responsive Web Design
```

也就是同一个 HTML 文件，根据屏幕宽度自动改变布局，而不是两个网页互相跳转。

不过因为你明确希望电脑和手机是两套独立页面，所以这版采用双页面方式。

将来如果网站开始做 SEO、投广告或接入统计，我建议再把两版合并为一个真正响应式页面。

## 发布到 GitHub Pages

1. GitHub 新建仓库，例如：
   `zelf-sale`

2. 上传这些文件到仓库根目录：
   - index.html
   - mobile.html
   - style.css
   - mobile.css
   - CNAME

3. 打开：
   Settings → Pages

4. Build and deployment：
   Source → Deploy from a branch

5. Branch：
   main

6. Folder：
   / (root)

7. Save

GitHub 会生成测试网址，例如：

```text
https://username.github.io/zelf-sale/
```

## 修改邮箱

在 `index.html` 和 `mobile.html` 中搜索：

```text
adam@zelf.com
```

全部替换成你的真实联系邮箱。

## 配置询盘

两个网页的表单都预留了 Formspree：

```text
https://formspree.io/f/xoevdrbw
```

在 Formspree 创建表单以后，把这个地址替换成你的真实 Form ID。

电脑和手机版可以共用同一个 Formspree 表单，这样所有买家询盘都会进入同一个邮箱。

## 绑定 Zelf.com

网站测试完成以后：

GitHub → Settings → Pages → Custom domain

填写：

```text
zelf.com
```

然后按照 GitHub Pages 当时显示的 DNS 指引，在你的域名注册商设置 A / CNAME 记录。

## 注意

设备识别永远不是 100% 准确，因为部分平板、折叠屏、桌面浏览器缩放、浏览器 UA 都可能特殊。

因此判断逻辑采用：

```text
User-Agent + 屏幕宽度
```

两者结合，比只判断 User-Agent 更可靠。
