# miku.new.tg 静态站部署步骤

## 一、上传到 GitHub

1. 登录 GitHub，点右上角 + → New repository。
2. 仓库名填 `miku-site`，选 Public，勾选 Add a README file，Create。
3. 进仓库 → Add file → Upload files，把本文件夹里的 `index.html` 拖进去，Commit changes。

## 二、开启 GitHub Pages

1. 仓库 → Settings → 左侧 Pages。
2. Source 选 `Deploy from a branch`，Branch 选 `main` + `/ (root)`，Save。
3. 等 1 分钟左右，页面顶部出现 `https://<用户名>.github.io/miku-site/`，打开确认能看到主页。
   - 如果仓库名就叫 `<用户名>.github.io`，地址会直接是 `https://<用户名>.github.io/`，更好看。

## 三、绑定自己的域名

1. 登录 DNSHE 控制台：https://my.dnshe.com/clientarea.php
2. 找到 `miku.new.tg` → 添加解析记录：
   - 类型：`CNAME`
   - 主机记录：`miku`（如果控制台要求填完整域名，就填 `miku.new.tg`）
   - 记录值：`<用户名>.github.io`
   - TTL：默认即可
3. 回到 GitHub 仓库 → Settings → Pages → Custom domain，填 `miku.new.tg`，Save。
4. 等 DNS 生效（几分钟），页面出现 Enforce HTTPS 勾选框后勾上，证书签发一般 5 分钟到 1 小时。

## 四、验证

- `https://miku.new.tg` 能打开且有小锁图标。
- 命令行验证解析：`nslookup miku.new.tg`
- 证书生效前如果提示不安全，先等一会儿，或点 Advanced → Proceed 临时查看。

## 常见问题

- **404**：Pages 还没部署完，或分支/目录选错；仓库里必须有 `index.html` 在根目录。
- **CNAME 填了但 GitHub 提示域名被占用**：检查是否已在别的仓库的 Pages 里设置过同一个域名。
- **HTTPS 一直签发失败**：通常是 DNS 还没生效，等 24 小时仍失败就把 Custom domain 删掉重填一次。
- **想换成真正的博客**：用 Hugo 或 Hexo 生成静态文件，把生成的 `public/` 内容覆盖到仓库根目录即可，域名配置不用改。
