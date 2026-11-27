# 这个目录是拿去放到公网上的

两个文件就够了：

| 文件 | 作用 |
|---|---|
| `index.html` | 页面本体（单文件，CSS/JS/词库全在里面） |
| `update.json` | App「检查更新」拉的就是它，告诉 App 新版本号是多少、页面叫哪个文件 |

App 里填的地址，就是这两个文件所在目录的**公开地址**，例如：

```
https://你的用户名.github.io/ship-english
```

填一次存在手机上，以后不用再动。

## GitHub Pages（推荐，电脑不用开）

1. 在 GitHub 建一个公开仓库，比如 `ship-english`
2. 在本机这个目录里：

```powershell
cd C:\Users\SU331\.dsh\profiles\desktop\ship-english\publish
git init
git add -A
git commit -m "init"
git remote add origin https://github.com/你的用户名/ship-english.git
git push -u origin main
```

3. 仓库 Settings → Pages → Source 选 `Deploy from a branch`，分支 `main`，目录 `/(root)`，保存
4. 等一分钟，浏览器打开 `https://你的用户名.github.io/ship-english/update.json`，
   能看到 `"version"` 就成了
5. App 里 ⚙ → 在线更新 → 地址填 `https://你的用户名.github.io/ship-english` → 检查更新

以后每次改完，在项目根目录跑一次 `\.\publish.ps1 -Push` 就发上去了。

## Gitee Pages（国内访问快）

流程一样，仓库建在 gitee.com，Pages 在「服务 → Gitee Pages」里开，地址形如
`https://你的用户名.gitee.io/ship-english`。首次开 Pages 需要实名。

## 对象存储（阿里云 OSS / 腾讯云 COS）

把这两个文件传到同一个 bucket 目录下，开静态网站托管，地址就是那个目录的访问域名。
注意把 `update.json` 的 Content-Type 设成 `application/json`。

## 注意

- `.nojekyll` 这个空文件别删：GitHub Pages 会跳过 Jekyll 处理，省掉一堆坑。
- APK 想一起放到公网，就把 `lunji-words.apk` 也扔进这个目录（`publish.ps1` 会自动带）。
- 页面是纯静态的，不需要任何后端。
