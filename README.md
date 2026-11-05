# Clarify for Mac: releases

Clarify is offline, push-to-talk dictation and voice control for Mac. Hold a key, speak, let go, and
clean text lands at your cursor. Recognition and cleanup run on your Mac, with the models inside the
app. There's no account. It's in beta, free, and the app's source isn't public.

**Get it from [clarifyfor.me](https://clarifyfor.me/).** That page describes every feature and says
which are in the beta, which need Clarify Pro and which aren't built yet.

Needs an Apple silicon Mac and macOS 14 or later. English only. The download is about 1.3 GB because
the models are inside it.

## What this repository is

It holds what Clarify's updater reads, and nothing else:

- [`appcast.xml`](appcast.xml): the list of versions the app checks. It's signed.
- [Releases](https://github.com/tamler/clarify-releases/releases): the notarized installers, with
  short notes. Recent notes also give the installer's SHA-256.

The installer on [Releases](https://github.com/tamler/clarify-releases/releases/latest) can be newer
than the one on clarifyfor.me. Either way, **Help > Check for Updates…** in the app brings you to
the latest.

## Check an installer

```sh
shasum -a 256 Clarify-<version>.dmg
spctl -a -t open --context context:primary-signature -vv Clarify-<version>.dmg
```

The first line should match the SHA-256 in that release's notes, if they give one. The second should
say `source=Notarized Developer ID`.

## What an update check sends

Clarify doesn't check for updates unless you choose **Check for Updates…** or turn on automatic
checks in **Settings > General**. A check is one request for `https://clarifyfor.me/appcast.xml`,
which redirects here. It has no identifier and no system profile, but clarifyfor.me and GitHub see
your IP address and Clarify's version. Nothing installs until you choose Install, and the app
refuses a list or a download without Clarify's signature.

## Problems and feedback

Use the Feedback link at the bottom of [clarifyfor.me](https://clarifyfor.me/). Include your Clarify
version (**Help > About Clarify**), your Mac and macOS version, and what happened. Leave out anything
private you dictated.
