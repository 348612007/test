# test

Git LFS + GitHub Actions 的最小可跑样例。

## 里面有什么

| 路径 | 作用 |
| --- | --- |
| `.gitattributes` | 声明 `*.bin` 等走 LFS |
| `assets/sample.bin` | 2 MiB 随机二进制，由 LFS 托管 |
| `assets/sample.sha256` | 该文件的 sha256，CI 里用来断言"拿到的是实体而不是指针" |
| `.github/workflows/lfs-check.yml` | 三条路径对照：`lfs: true` / 不带 lfs / 手动 `git lfs pull` |

## 关键结论

`actions/checkout` **默认不拉 LFS 对象**。不加 `lfs: true` 时，工作区里的 `assets/sample.bin`
是一个 130 字节左右的指针文本；加了之后才是 2 MiB 真文件。

```yaml
- uses: actions/checkout@v4
  with:
    lfs: true
```
