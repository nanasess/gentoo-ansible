# CLAUDE.md

このファイルは、このリポジトリでコードを操作する際にClaude Code (claude.ai/code) にガイダンスを提供します。

## よく使用するコマンド

### Ansible操作
- **ドライラン**: `ansible-playbook playbook.yml --ask-become-pass --check --diff`
- **デプロイ**: `ansible-playbook playbook.yml --ask-become-pass`

## アーキテクチャ

これはAnsibleを使用したGentoo Linuxの構成管理リポジトリです。主な目的は、WSL（Windows Subsystem for Linux）で動作するGentooシステムのセットアップと保守を自動化することです。

### 主要コンポーネント

**メインプレイブック** (`playbook.yml`):
- localhostで管理者権限を使用して実行
- Portage設定ファイルを管理
- `portage`モジュールを使用してパッケージをインストール
- PHP開発用のComposerをセットアップ

**Portage設定** (`etc/portage/`):
- `make.conf`: WSL固有の設定を含むコアPortage設定（VIDEO_CARDS="d3d12"）
- `package.use/`: 特定のパッケージ用のUSEフラグ設定を含むディレクトリ
- `package.accept_keywords`: パッケージキーワード受け入れルール
- `package.mask`: パッケージマスクルール
- `package.license`: ライセンス受け入れ設定

**システム設定**:
- WSL固有の設定ファイル（`etc/wsl.conf`、`etc/tmpfiles.d/wsl.conf`）

### パッケージ管理戦略

プレイブックは以下を含む包括的な開発環境をインストールします：
- 開発ツール（git、vim、emacs、ripgrep、github-cli）
- 言語ランタイム（nodejs、php、python、ruby、java、dotnet）
- システムユーティリティ（sudo、zsh、fzf、eza）
- マルチメディアツール（ffmpeg）
- クラウドツール（terraform、awscli、google-cloud-cli）
- データベースクライアント（pgcli、litecli、mycli）

パッケージリストを変更する際は、パッケージがGentooのメインリポジトリまたは設定されたオーバーレイ（1password用のjaredallardオーバーレイなど）で利用可能であることを確認してください。