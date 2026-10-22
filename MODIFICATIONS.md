# Modifications vs upstream SmartTube

Upstream base: **yuliskov/SmartTube, version 32.68 (Beta)**
Upstream repo: https://github.com/yuliskov/SmartTube

This fork changes exactly two source locations. Everything else is
verbatim upstream.

## 1. Home tab content = Subscriptions feed

File:
`common/src/main/java/com/liskovsoft/smartyoutubetv2/common/app/presenters/BrowsePresenter.java`
(method `initRowAndGridMapping()`)

Upstream:

```java
mRowMapping.put(MediaGroup.TYPE_HOME, getContentService().getHomeObserve());
```

Modified (marked with a `// FRY MOD v2:` comment in the source; this is
the current v2 form — v1 returned the single group unsplit):

```java
mRowMapping.put(MediaGroup.TYPE_HOME, getContentService().getSubscriptionsObserve()
        .map(mediaGroup -> {
            List<MediaGroup> groups = new ArrayList<>();
            if (mediaGroup == null || mediaGroup.getMediaItems() == null) {
                if (mediaGroup != null) {
                    groups.add(mediaGroup);
                }
                return groups;
            }
            List<MediaItem> liveItems = new ArrayList<>();
            List<MediaItem> recentItems = new ArrayList<>();
            for (MediaItem item : mediaGroup.getMediaItems()) {
                if (item == null) {
                    continue;
                }
                if (item.isLive() || item.isUpcoming()) {
                    liveItems.add(item);
                } else {
                    recentItems.add(item);
                }
            }
            if (liveItems.isEmpty() || recentItems.isEmpty()) {
                groups.add(mediaGroup);
                return groups;
            }
            YouTubeMediaGroup liveGroup = new YouTubeMediaGroup(MediaGroup.TYPE_HOME);
            liveGroup.setTitle("訂閱直播");
            liveGroup.setMediaItems(liveItems);
            YouTubeMediaGroup recentGroup = new YouTubeMediaGroup(MediaGroup.TYPE_HOME);
            recentGroup.setTitle("最近上載");
            recentGroup.setMediaItems(recentItems);
            groups.add(liveGroup);
            groups.add(recentGroup);
            return groups;
        }));
```

The `.map(...)` adapter is required because the row mapping expects
`Observable<List<MediaGroup>>` while `getSubscriptionsObserve()` emits
`Observable<MediaGroup>` (a single feed group). The v2 mapper splits
that group into two rows — live/upcoming items and everything else in
feed order — falling back to the single original group when one side is
empty. No sidebar section is added, removed, or renamed; only the Home
tab's content source changes.

## 2. Update channel = this repository

File: `common/src/stbeta/res/values/update_urls.xml`

Upstream Beta reads its update manifest from
`https://github.com/yuliskov/SmartTubeNext/releases/download/latest/smarttube_beta2.json`.

This fork points the single entry at the fork maintainer's manifest
endpoint. That manifest keeps upstream's JSON format
(`package.downloadUrlList*` plus one entry per version with
`versionCode`/`changelog`), and its download entries resolve to the
APK published in this repository on the `release` branch
(`SmartTube-Beta-Mod.apk`, alongside a copy of the manifest,
`smarttube-beta-mod.json`). The built-in updater therefore works
unchanged and installs this fork's builds, served from this repo.

## Build

Standard upstream build for the Beta flavor:

```
./gradlew assembleStbetaRelease
```

* JDK 17, Android SDK platform 34, build-tools 33.0.2 / 34.0.0.
* Signing: provide a `keystore.properties` in the project root (upstream
  mechanism) with your own keystore. Release builds of this fork are
  signed with the fork maintainer's key, which is why they cannot be
  installed over official Beta builds (different signature, same
  package name `org.smarttube.beta`).
* Published artifact: the `universal` APK from
  `smarttubetv/build/outputs/apk/stbeta/release/`.
