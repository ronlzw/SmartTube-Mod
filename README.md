# SmartTube — Subscriptions Home (Modified Version)

> **Unofficial modified version.** This project is a modified version of
> [SmartTube](https://github.com/yuliskov/SmartTube) by **yuliskov**.
> It is **not** affiliated with, endorsed by, or connected to the original
> author. All credit for the original application goes to yuliskov and the
> SmartTube contributors.

## What is different from the original?

Based on upstream **SmartTube 32.68 (Beta channel)**, this build changes
exactly two things:

1. **Home shows subscriptions only.** The Home tab keeps its original
   layout and all sidebar sections, but its video content comes from the
   signed-in account's **Subscriptions** feed instead of YouTube's
   recommended feed, arranged in two rows: the first row, “Home”, is
   led by older videos, with newer uploads from deeper in the feed mixed
   in at a 3:2 ratio; the second row, “Latest uploads”, shows the 30
   newest uploads. Live streams and upcoming premieres never appear on
   Home — so a child using this build only sees videos from channels the
   account is subscribed to.
2. **In-app updates point to this repository.** The built-in update
   checker reads its update manifest from this repo (served from the
   `release` branch, not from upstream), so "update" inside the app
   installs the newest build of *this modified version*.

Nothing else is changed. Search, channels, playback, history and all
other features behave exactly like upstream.

Details for developers are in [MODIFICATIONS.md](MODIFICATIONS.md).
The original upstream readme is preserved as
[README.upstream.md](README.upstream.md).

## Install

Download the universal APK `SmartTube-Beta-Mod.apk` from the
[`release` branch](../../tree/release) and install it on the Android TV.
Package name is `org.smarttube.beta` (same as upstream Beta), so it
coexists with SmartTube Stable — but because it is signed with a
different key, it cannot be installed over the official Beta: back up
your data inside the official Beta first (Settings → Backup), uninstall
it, install this build, then restore the backup.

## License

This project is licensed under the **GNU General Public License v3.0**,
the same license as the original SmartTube — see [LICENSE](LICENSE).
The complete source code of this modified version is published in this
repository, as required by the GPL. Original copyright notices are
preserved throughout the source tree.

---

## 中文说明

这是 **SmartTube 的非官方改版**，原版作者为 yuliskov
（https://github.com/yuliskov/SmartTube），本项目与原作者无关。

基于原版 **32.68（Beta）**，只改动两处：

1. **首页只显示订阅视频**——首页排版与栏目不变，内容改为来自账号
   「订阅」的视频，并拆成两行：第一行「首页」以旧片为主，旧片与订阅源
   较深处的新片按 3:2 穿插；第二行「最新上传」显示最新 30 条新片；
   直播与预告一律不出现在首页，不再显示
   YouTube 推荐内容，避免孩子看到杂乱的推荐视频。
2. **App 内在线更新指向本仓库**——点击更新会升级到本改版的新版本，
   不会升回官方版本；更新文件通过本仓库的 `release` 分支发布。

其余功能与原版完全相同。授权与原版同为 GPL-3.0，改版源码已按授权
要求全部公开于本仓库。
