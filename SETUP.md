# Floci GCP Tutorial — Setup Guide

This guide prepares your machine for the Floci GCP tutorial.

Floci provides a local GCP emulator that can be used without a Google Cloud account, authentication token, or billing account. The emulator exposes GCP-shaped services locally, with the GCP endpoint normally available at `http://localhost:4588`. citeturn0search4

> **Important:** This setup is for learning and local practice. Do **not** create a Google Cloud billing account or run `gcloud auth login` just to use Floci locally.

---

## Prerequisites

You need:

- Docker / Docker Desktop
- Google Cloud CLI (`gcloud`)
- A terminal appropriate for your operating system

Floci's current GCP installation documentation recommends Docker and requires Docker 20.10+ and Docker Compose v2+ when using Compose. citeturn0search2

---

# Windows 11 — Recommended Setup

The Windows instructions below are intentionally written for **PowerShell**.

## 1. Install Docker Desktop

Install Docker Desktop for Windows and make sure Docker is running.

Verify:

```powershell
docker --version
docker info
```

You should see Docker client/server information without an error.

## 2. Install Google Cloud CLI

Install the Google Cloud CLI using Google's official Windows installation instructions. citeturn0search7turn0search10

After installation, open a **new PowerShell window** and verify:

```powershell
gcloud --version
```

> **Do not run `gcloud auth login` for this Floci-only setup.** Authentication is not required by the local emulator.

## 3. Start Floci GCP

You can run the emulator directly with Docker:

```powershell
docker run --rm -p 4588:4588 floci/floci-gcp:latest
```

Keep this terminal open while using the emulator.

Floci's official documentation also supports managing the emulator through the Floci CLI. On Windows PowerShell, the official Floci CLI installation command is: citeturn0search0turn0search1

```powershell
iwr https://floci.io/install.ps1 | iex
```

Then:

```powershell
floci gcp start
```

## 4. Verify the emulator

Open a second PowerShell window:

```powershell
Test-NetConnection localhost -Port 4588
```

Look for:

```text
TcpTestSucceeded : True
```

A simple HTTP check can also be performed with:

```powershell
curl.exe -i http://localhost:4588/
```

A `404 Not Found` response at `/` is not by itself a problem. The important part is that the local server is reachable.

## 5. Configure `gcloud` for Floci

Set the local Storage API endpoint:

```powershell
$env:CLOUDSDK_API_ENDPOINT_OVERRIDES_STORAGE="http://localhost:4588/"
$env:CLOUDSDK_CORE_PROJECT="floci-local"
```

For the current PowerShell session, disable Google Cloud credential loading:

```powershell
gcloud config set auth/disable_credentials true
```

Set the local account/project identifiers used by the tutorial:

```powershell
gcloud config set account floci-local
gcloud config set project floci-local
```

Verify:

```powershell
gcloud config list
```

You should see values similar to:

```text
[api_endpoint_overrides]
storage = http://localhost:4588/

[auth]
disable_credentials = true

[core]
account = floci-local
project = floci-local
```

Then test Cloud Storage:

```powershell
gcloud storage buckets list
```

An empty result such as `Listed 0 items.` means the local Storage service is reachable and there are currently no buckets.

## 6. Create your first local bucket

```powershell
gcloud storage buckets create gs://my-bucket
```

Then:

```powershell
gcloud storage buckets list
```

You should now see `my-bucket`.

## 7. PowerShell equivalents of common Unix commands

Some Floci documentation uses Unix shell syntax. On Windows PowerShell, use the following equivalents when needed:

| Unix-style command | PowerShell equivalent |
|---|---|
| `export NAME=value` | `$env:NAME="value"` |
| `echo "text" > file.txt` | `"text" \| Set-Content file.txt` |
| `cat file.txt` | `Get-Content file.txt` |
| `eval $(floci gcp env)` | `floci gcp env --shell powershell \| Invoke-Expression` |

The Floci CLI supports PowerShell environment output. citeturn0search9

---

# macOS

Use the standard Floci and Google Cloud CLI installation methods for macOS.

## 1. Install Docker

Install Docker Desktop for Mac and verify:

```bash
docker --version
docker info
```

## 2. Install Floci CLI

Floci documents Homebrew and the installation script for macOS: citeturn0search0turn0search1

### Homebrew

```bash
brew install floci-io/floci/floci
```

Or:

```bash
curl -fsSL https://floci.io/install.sh | sh
```

## 3. Install Google Cloud CLI

Install the Google Cloud CLI using Google's official macOS/Linux installation documentation. citeturn0search10

Verify:

```bash
gcloud --version
```

## 4. Start Floci GCP

```bash
floci gcp start
```

## 5. Export the Floci environment

```bash
eval $(floci gcp env)
```

Floci's GCP CLI exports emulator endpoints for services including Storage, Pub/Sub, Firestore, Datastore, and Secret Manager. citeturn0search0turn0search9

## 6. Configure the Storage endpoint

If using `gcloud` Storage commands directly:

```bash
export CLOUDSDK_API_ENDPOINT_OVERRIDES_STORAGE=http://localhost:4588/
export CLOUDSDK_CORE_PROJECT=floci-local
```

Then test:

```bash
gcloud storage buckets list
```

---

# Linux

Use the standard Docker, Floci CLI, and Google Cloud CLI installation methods for your Linux distribution.

## 1. Install Docker

Install Docker Engine or Docker Desktop according to your distribution and verify:

```bash
docker --version
docker info
```

## 2. Install Floci CLI

Floci provides an installation script for Linux: citeturn0search0turn0search1

```bash
curl -fsSL https://floci.io/install.sh | sh
```

Alternatively, with Homebrew:

```bash
brew install floci-io/floci/floci
```

## 3. Install Google Cloud CLI

Follow Google's official Google Cloud CLI installation instructions for your Linux distribution. citeturn0search10

Verify:

```bash
gcloud --version
```

## 4. Start Floci GCP

```bash
floci gcp start
```

## 5. Export the Floci environment

```bash
eval $(floci gcp env)
```

## 6. Configure the Storage endpoint

```bash
export CLOUDSDK_API_ENDPOINT_OVERRIDES_STORAGE=http://localhost:4588/
export CLOUDSDK_CORE_PROJECT=floci-local
```

Test:

```bash
gcloud storage buckets list
```

---

# Troubleshooting with AI

If you face **any issue during setup**, do not spend hours trying random fixes.

Copy the following prompt into ChatGPT, Claude, Gemini, or another AI assistant and include the command you ran and the **complete error/output**.

```text
I am setting up the Floci GCP local emulator so I can learn Google Cloud without using a real GCP billing account.

My operating system is: <Windows 11 / macOS / Linux>

My goal:
- Run Floci GCP locally
- Use the Google Cloud CLI (gcloud) against the local emulator
- Practice GCP services without authenticating to a real Google Cloud account

Floci should be running locally on port 4588.

Please help me troubleshoot the setup step by step.

Important rules:
1. Do NOT tell me to create a Google Cloud free trial or billing account unless the specific problem genuinely requires real GCP.
2. Do NOT tell me to run `gcloud auth login` for the Floci-local setup unless you first explain why it is necessary.
3. Do not assume anything about my machine.
4. Ask me to run diagnostic commands when information is missing.
5. Give me one step at a time and wait for my output before moving to the next step.
6. Explain what each command is checking or changing.

Here is the command I ran:

<PASTE COMMAND HERE>

Here is the complete output/error:

<PASTE COMPLETE OUTPUT HERE>

Please diagnose the problem and give me the next exact command to run.
```

---

# Setup Complete

Once your setup works, you should be able to run GCP-style commands against the local Floci emulator without a real GCP billing account.

For example:

```bash
gcloud storage buckets list
```

The next step is to follow the tutorial chapters in `CHAPTERS.md`.

## Official references

- Floci GCP: https://floci.io/gcp/
- Floci GCP installation: https://floci.io/floci-gcp/getting-started/installation/
- Floci GCP GitHub: https://github.com/floci-io/floci-gcp
- Floci CLI: https://github.com/floci-io/floci-cli
- Google Cloud CLI installation: https://cloud.google.com/sdk/docs/install
