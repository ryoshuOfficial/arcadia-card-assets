# Arcadia Card Assets

《阿尔卡迪亚》AI 世界卡的静态资源仓库。

配合 **jsDelivr** 使用：文件 push 上来之后，会自动获得一个全球 CDN 直链，
**自带 CORS 与 Range 支持**，可以直接放进角色卡的 `<audio src="...">`。

---

## 目录

```
music/
  cossack-song.m4a   哥萨克之歌 · 用于「哥萨克骑兵营」通用事件
```

---

## 链接格式

```
https://cdn.jsdelivr.net/gh/<你的GitHub用户名>/arcadia-card-assets@main/music/cossack-song.m4a
```

**换成你的用户名即可。** 例如用户名是 `yourname`：

```
https://cdn.jsdelivr.net/gh/yourname/arcadia-card-assets@main/music/cossack-song.m4a
```

### 关于 `@main`

- `@main` = 跟随主分支，**改了文件链接不变，但 jsDelivr 有约 7 天缓存**，更新后不会立刻生效
- `@<commit-hash>` = 锁定到某一个提交，**永久不变、缓存友好**，适合正式发布
- `@v1.0.0`（tag）= 语义化版本，推荐正式发布用这个

**建议**：调试时用 `@main`，正式发布时打个 tag 用 `@v1.0.0`，这样以后加音乐也不会影响已发布的卡。

---

## 已验证的能力（实测数据）

| 项目 | 结果 |
|---|---|
| HTTP | `200` |
| CORS | `Access-Control-Allow-Origin: *` |
| 跨域资源策略 | `Cross-Origin-Resource-Policy: cross-origin` |
| Range 请求 | `206` + `Content-Range: bytes 0-1023/...` |
| 缓存 | `public, max-age=604800` |
| 单文件大小上限 | **20 MB**（当前文件 729 KB，余量充足） |

---

## 加新文件

```bash
# 放进对应目录（文件名建议只用 ASCII：字母、数字、连字符）
cp 新音乐.m4a music/new-track.m4a

git add .
git commit -m "add new-track"
git push
```

然后链接就是：

```
https://cdn.jsdelivr.net/gh/<用户名>/arcadia-card-assets@main/music/new-track.m4a
```

**文件名请避免**：空格、中文、方括号 `[ ]`、俄文字母。
这些字符在 URL 里需要转义，不同 CDN 的处理方式不一致，容易出 404。

---

## 注意事项

- **仓库必须是 Public**，jsDelivr 无法读取私有仓库
- 单个文件 **不要超过 20 MB**
- 音频建议用 `.m4a` 或 `.mp3`：
  - `.m4a` 会被识别为 `audio/mp4`
  - `.mp3` 会被识别为 `audio/mpeg`
  - 不要用 `.aac` 后缀装 MP4 容器（虽然能播，但 MIME 会不对）

---

## 授权提醒

`cossack-song.m4a` 为《边狱巴士》(Limbus Company) 相关音乐素材。
非营利同人使用前请自行确认授权范围，并在卡片中注明来源。
