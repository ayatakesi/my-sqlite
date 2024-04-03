# sqlite3
GNU Emacs30.0.50に含まれる`java/INSTALL`にしたがってパッチを適用したsqlite3モジュール)のレポジトリ。

# 作成した手順
1. [Google Gitのsqlite3](https://android.googlesource.com/platform/external/sqlite)をclone


```bash
$: git clone https://android.googlesource.com/platform/external/sqlite
```

2. デフォルトの`main`ブランチのコミット`f63e8d96e298783c310c08030d4c51a875dae4cd`をcheckoutして[^1]、修正用ブランチ`my/main`をcut

```bash
$: cd sqlite
$: git checkout f63e8d96e298783c310c08030d4c51a875dae4cd
$: git checkout -b my/main
```

3. `java/INSTALL`にしたがいpatchを適用

```bash
$: patch -p1 < PATCH_FOR_SQLITE3.patch
```

4. 上記patch ファイルとpatch適用後ファイルをcommitして空レポジトリにpush

```bash
$: git add -A
$: git commit -m 'nanika commit messages...'
$: gh repo create my-sqlite --public
$: git remote add mine https://github.com/JIBUN/my-sqlite.git
$: git branch -M my/main
$: git push -u mine my/main
```
[^1]: 他のモジュールのように`nougat-...`ではビルドできなかったので(詳細は失念)、`java/INSTALL`のpatchに記載されていた`LOCAL_SDK_VERSION := 23`を手掛かりにコミットhashを特定したら上手くビルドできたので、そのまま使用しています。
