
### Install

1. Add keybase/beta tap (only need to do this once):

          brew tap keybase/beta
          
1. Update brew (formulas change a lot):

          brew update

1. To install Keybase:

| Env     | Command                             | Executable | Notes
| ------- | ----------------------------------- | ---------- | -----
| Prod    | `brew install keybase/beta/keybase` | `keybase`  | This is temporarily disabled until prod is safe.
| Staging | `brew install keybase/beta/kbstage` | `kbstage`  |
| Devel   | `brew install keybase/beta/kbdev`   | `kbdev`    |


To (force) install Keybase from source (this is default if there is no bottle), use `--build-from-source`. For example:

          brew install --build-from-source keybase/beta/kbstage

### Updating the Formula

This example assumes the version is `1.0.0-15`.

- Edit the source archive URL:

          https://github.com/keybase/client-beta/archive/v1.0.0-15.tar.gz

- Download the source archive and calculate the sha256:

          wget https://github.com/keybase/client-beta/archive/v1.0.0-15.tar.gz
          shasum -a 256 v1.0.0-15.tar.gz

- Update the formula version:

          version "1.0.0-15"

- Comment out the bottle section. We will update it later.
- Commit and push the changes.
- Update your taps: `brew update`. You should see keybase in the list of updated formula.

### Bottling

    brew uninstall keybase
    brew install --build-bottle keybase/beta/keybase
    brew postinstall keybase/beta/keybase
    brew bottle keybase/beta/keybase

Copy the bottle into the formula. In the bottle block, update the root_url for the bottle section of keybase.rb and push to the repo. It doesn't include the `tar.gz` file name:

    root_url "https://github.com/keybase/client-beta/releases/download/v1.0.0-15/"

In the `keybase/client-beta` repository, draft a new release. Select the correct/matching tag version from the drop down.
Update the release title (you can use the version `v1.0.0-15`) and description should include changes from the previous release. Then upload the `keybase-1.0.0-15.yosemite.bottle.tar.gz` file, mark pre-release and hit Publish.

Commit and push the changes. After pushing, update your tap: `brew update`.

Then try testing the bottle by uninstalling and re-installing.
