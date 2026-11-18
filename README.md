# firefox-ipa
Repo to store the workflow for creating a firefox ipa for sideloading

A GitHub Actions workflow ([build-ipa.yml](.github/workflows/build-ipa.yml)) that builds an unsigned
device IPA of [Firefox for iOS](https://github.com/mozilla-mobile/firefox-ios) on a GitHub-hosted
macOS runner, so it can be installed with SideStore alongside the App Store Firefox. No Mac needed.

## Usage

1. Actions → **Build Firefox iOS IPA** → **Run workflow**.
2. Download the `firefox-ios-<ref>` artifact, unzip it, and open `Firefox.ipa` in SideStore.

### Inputs

| Input | Default | Notes |
| --- | --- | --- |
| `ref` | `firefox-v160.1` | Tag or branch of firefox-ios to build ([releases](https://github.com/mozilla-mobile/firefox-ios/releases)). |
| `team_id` | empty | Your 10-character Apple Team ID (the suffix SideStore adds to sideloaded bundle IDs). Lets saved logins and Firefox Sync use the keychain. |
| `display_name` | `Firefox 2` | Home-screen name. |
| `keep_extensions` | `false` | Keep widgets, share sheet, autofill and other extensions. Each one uses up a free-account App ID (10 per week). |
| `xcode_version` | `27.1` | Must match the Xcode badge in the firefox-ios README for the chosen `ref`. |

## Notes

- The workflow runs on the `xcode-27` runner image (public preview). If GitHub renames it, update `runs-on`.
- Keep the repo public: macOS runner minutes are free for public repos, while private repos burn
  through the free quota at a 10x rate.
- Free Apple accounts can't use push notifications or the default-browser entitlement, so those features won't work.
- If a build fails, the full `xcodebuild` log is uploaded as the `xcodebuild-log` artifact.
