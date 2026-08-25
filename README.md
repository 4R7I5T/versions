# BioLLM Studio — update metadata

This repository contains **no source code**. It holds only the update manifests that an
installed copy of BioLLM Studio polls to discover whether a newer build exists.

Each file is a small JSON document at a path like:

    stable/win32/x64/system/latest.json
    stable/darwin/arm64/latest.json

and contains only:

| field | meaning |
| --- | --- |
| `url` | where to download the update from |
| `name` | the release version |
| `version` | the source commit the build came from |
| `productVersion` | the version shown in the application |
| `timestamp` | when the manifest was written |
| `sha1hash`, `sha256hash` | checksums of the asset, so a client can verify what it downloaded |

## Why this repository is public

The updater runs inside an installed application on a user's machine. It has no GitHub
credentials, so it fetches these manifests over `raw.githubusercontent.com`
unauthenticated. A private repository returns 404 to that request, and updates would
never be discovered.

Publishing checksums and download URLs is the point of the file — it is what lets a
client verify an update. The application's source remains in its own private repository.

Written automatically by `update_version.sh` during a release. Do not edit by hand.
