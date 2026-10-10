# falk

Official public binaries and installers for falk. The product source repository is private. This repository contains only distribution documentation and black-box release validation.

## Install

macOS/Linux:

```sh
curl -q --proto '=https' --tlsv1.2 -fsSL https://github.com/bai-os/falk-releases/releases/latest/download/install.sh | sh
```

Windows PowerShell:

```powershell
Invoke-WebRequest -UseBasicParsing https://github.com/bai-os/falk-releases/releases/latest/download/install.ps1 -OutFile install-falk.ps1
# Review the script, then run it:
./install-falk.ps1
```

Installers select the OS/processor and verify version-pinned SHA-256 checksums. Unix uses `~/.local/bin`; Windows uses `%LOCALAPPDATA%\falk\bin` and adds it to user PATH. Unix prints a PATH instruction if needed. No sudo, source checkout, Go or Bun is required.

## Update

```sh
falk update --check
falk update
falk update --version 0.1.0
```

Updates require signed release metadata and exact executable checksums/platform/version. Default follows stable releases without downgrading; explicit versions permit rollback. Workspace, server and login are retained. No falk credential is sent to the release channel.

## Sign in

Your administrator supplies your team server and workspace:

```sh
falk setup --api-url <team-https-origin> --workspace-id <workspace-id>
falk login
falk status
```

Binary installation does not grant product access.

## Verification

`release-public-key.txt` is the Ed25519 release trust root. `manifest.sig` is a Base64 Ed25519 signature over `falk-cli-release-v2\n` followed by the exact `manifest.json` bytes. Install/update/rollback are checked on all six native OS/CPU targets by the public validation workflow. Candidate releases are prereleases and do not become stable latest until these checks pass.
