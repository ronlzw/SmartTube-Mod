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

Modified (marked with a `// FRY MOD:` comment in the source):

```java
mRowMapping.put(MediaGroup.TYPE_HOME, getContentService().getSubscriptionsObserve()
        .map(mediaGroup -> {
            List<MediaGroup> groups = new ArrayList<>();
            if (mediaGroup != null) {
                groups.add(mediaGroup);
            }
            return groups;
        }));
```

The `.map(...)` adapter is required because the row mapping expects
`Observable<List<MediaGroup>>` while `getSubscriptionsObserve()` emits
`Observable<MediaGroup>` (a single feed group). No sidebar section is
added, removed, or renamed; only the Home tab's content source changes.

## 2. Update channel = this repository

File: `common/src/stbeta/res/values/update_urls.xml`

Upstream Beta reads its update manifest from
`https://github.com/yuliskov/SmartTubeNext/releases/download/latest/smarttube_beta2.json`.

This fork points the single entry at this repo's own manifest asset:

```
https://github.com/<owner>/<repo>/releases/download/latest/smarttube-beta-mod.json
```

The manifest keeps upstream's JSON format (`package.downloadUrlList*`
plus one entry per version with `versionCode`/`changelog`), so the
built-in updater works unchanged and installs builds published in this
repo's Releases.

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
