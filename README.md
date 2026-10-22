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
   recommended feed — so a child using this build only sees videos from
   channels the account is subscribed to.
2. **In-app updates point to this repository.** The built-in update
   checker reads its update manifest from this repo's GitHub Releases
   (not from upstream), so "update" inside the app installs the newest
   build of *this modified version*.

Nothing else is changed. Search, channels, playback, history and all
other features behave exactly like upstream.

Details for developers are in [MODIFICATIONS.md](MODIFICATIONS.md).
The original upstream readme is preserved as
[README.upstream.md](README.upstream.md).

## Install

Download the universal APK from the
[Releases](../../releases) page and install it on the Android TV.
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

呢个系 **SmartTube 嘅非官方改版**，原版作者系 yuliskov
（https://github.com/yuliskov/SmartTube），本项目同原作者无关。

基于原版 **32.68（Beta）**，只改两样嘢：

1. **首页只显示订阅视频**——首页排版同栏目不变，但内容改成嚟自账号
   「订阅」嘅视频，唔再显示 YouTube 推荐俾小朋友睇到杂乱内容。
2. **App 内在线更新改指本仓库**——点更新会升到呢个改版嘅新版本，
   唔会升返官方版本。

其余功能同原版完全一样。授权跟原版同为 GPL-3.0，改版源码已按授权
要求全数公开喺本仓库。
