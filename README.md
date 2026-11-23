# CookCLI for TOS 7 (Deb)

把纯文本 .cook 食谱变成在线食谱库：浏览、搜索、按份数缩放、生成购物清单，也可以直接在网页里编辑食谱。食谱文件以普通文本保存在 NAS 共享文件夹中。

Turns plain-text .cook recipes into a browsable cookbook: browse, search, scale by servings and build shopping lists, and edit recipes right in the web UI. Recipes stay ordinary text files in a NAS shared folder.

## Package

- Application ID: `cookcli`
- Type: Deb single package (TOS 7)
- Architecture: `x86_64`, `aarch64`
- Backend: static binary from the upstream release, run as a systemd service
- Web UI: served at `/<app_id>/` through the TOS nginx entry
- Recipe folder: the `cookcli-data` NAS shared folder, or the package data directory

## Source

The `src/` directory contains the files the package is built from:

- `src/config.x86_64.ini` / `src/config.aarch64.ini` — `config.ini` per architecture
- `src/cookcli.lang` — 14 language sections
- `src/cookcli.svg` — application icon

The package tree itself (service unit, nginx location, maintainer scripts) is
produced by `build_deb.py` in the build toolchain.

Build toolchain: https://github.com/Irvingfei/tos-docker-apps

## Install

1. In the TOS App Center, add this repository's application and submit the matching `cookcli_<arch>.deb` asset from the latest Release.
2. Recipes live in the shared folder the package creates; drop `.cook` files there over SMB or the File Manager.

## Notes

食谱保存在 NAS 共享文件夹 cookcli-data 的 recipes 子目录中，可直接通过文件管理器或 SMB 增删修改。默认不启用登录，同一网络内能访问本机的人都可以查看和修改食谱；如需限制，请在 NAS 防火墙中限制 18087 端口。网页地址为 http://NAS地址/cookcli/。

This repository packages the upstream open-source application for TerraMaster TOS 7.
It is not affiliated with or endorsed by the upstream project. Application names and
trademarks belong to their respective owners.
