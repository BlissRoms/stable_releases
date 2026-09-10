<p align="center">
  <img src="banner.png" alt="BlissRoms Banner">
</p>

<p align="center">
  <a href="https://blissroms.org">Website</a> |
  <a href="https://blissroms.org/downloads">Download</a> |
  <a href="https://docs.blissroms.org">Documentation</a> |
  <a href="https://blissroms.org/blog">Blog</a> |
  <a href="https://github.com/BlissRoms">GitHub</a>
</p>

<p align="center">
  <a href="https://t.me/BlissROM_Updates">Telegram Channel</a> |
  <a href="https://t.me/Team_Bliss_Community">Telegram Community</a> |
  <a href="https://twitter.com/bliss_roms">Twitter</a> |
  <a href="https://mastodon.social/@blissroms">Mastodon</a> |
  <a href="https://bsky.app/profile/blissroms.bsky.social">Bluesky</a> |
  <a href="https://www.instagram.com/blissroms">Instagram</a> |
  <a href="https://www.facebook.com/BlissROMs">Facebook</a>
</p>

<p align="center">
  <a href="https://opencollective.com/blissroms">Donate via OpenCollective</a>
</p>

## BlissRoms - Waterlily (Android 16)

An open-source Android ROM project by [BlissLabs](https://blissroms.org), focused on providing a clean, stable, and feature-rich Android experience. Built on [AOSP](https://android.googlesource.com) with carefully selected enhancements and optimizations.

Please read the [AOSP building instructions](https://source.android.com/source/index.html) before proceeding.

---

## Requirements

- **OS:** Latest [Ubuntu LTS](https://www.ubuntu.com/download/server) release (24.04 recommended)
- **CPU:** Hexa-core or better recommended
- **RAM:** 64GB (consider more for virtual machines)
- **Storage:** 500GB+ free disk space (~100GB for repo sync, expands to ~250GB, plus build output)
- **Java:** OpenJDK 21
- **Python:** Python 3

---

## Installing Java 21

```bash
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install openjdk-21-jdk
sudo update-alternatives --config java   # Make sure Java 21 is selected
sudo update-alternatives --config javac  # Make sure Java 21 is selected
```

---

## Installing `repo`

```bash
mkdir -p ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

Make sure `~/bin` is in your `PATH`:

```bash
echo 'export PATH=~/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

---

## Grabbing Dependencies

```bash
sudo apt-get install git-core gnupg flex bison gperf build-essential zip curl \
    zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses-dev \
    x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev \
    libxml2-utils xsltproc unzip squashfs-tools python3-mako libssl-dev \
    ninja-build lunzip syslinux syslinux-utils gettext genisoimage bc \
    xorriso xmlstarlet git-lfs rsync
```

---

## Initializing Repository

**Repo initialization:**

```bash
repo init -u https://github.com/BlissRoms/stable_releases.git -b waterlily --git-lfs
```

**Sync repo:**

```bash
repo sync -c --force-sync --no-tags --no-clone-bundle -j$(nproc) --optimized-fetch --prune
```

---

## Build Options

`BLISS_BUILD_VARIANT` - (vanilla, gapps, foss, microg) - Specifies what type of extra apps and services to include in the build.

> **Note:** Default `BLISS_BUILD_VARIANT` is **VANILLA**.

---

## Building

```bash
. build/envsetup.sh
blissify [options] <deviceCodename>
```

**Options:**

| Flag | Description |
|------|-------------|
| `-h` / `--help` | Show the help dialog |
| `-c` / `--clean` | Clean up before running the build |
| `-d` / `--devclean` | Clean up device tree only before running the build |
| `-v` / `--vanilla` | Build with no added app store solution *(default)* |
| `-g` / `--gapps` | Build with Minimal Google Play Services added |
| `-f` / `--foss` | Build with FOSS (arm64-v8a) app store solutions added *(requires vendor/foss)* |
| `-m` / `--microg` | Build with MicroG |

**Examples:**

```bash
# Build with GApps
blissify -g deviceCodename

# Build with FOSS
blissify -f deviceCodename

# Build with GApps and device clean
blissify -g -d deviceCodename

# Vanilla build (legacy-compatible)
blissify deviceCodename
```

---

## Report Build Issues

- [Telegram - Build Support](https://t.me/Team_Bliss_Build_Support)
- [Telegram - Community](https://t.me/Team_Bliss_Community)
