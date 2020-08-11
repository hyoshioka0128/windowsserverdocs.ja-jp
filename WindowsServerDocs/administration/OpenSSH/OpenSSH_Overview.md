---
title: Windows 用 OpenSSH の概要
description: Linux とその他の Windows 以外の管理者によって、リモート システムのクロスプラットフォーム管理用に使用される OpenSSH ツールの概要。
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendmsft
ms.type: conceptual
ms.openlocfilehash: 1c0686d7bbe6e78baf924919c6733b733fe65f64
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879494"
---
# <a name="openssh-in-windows"></a>Windows での OpenSSH

OpenSSH は、Linux と非 Windows の管理者が、リモート システムのクロスプラットフォーム管理を行うために使用するオープンソース バージョンの Secure Shell (SSH) ツールです。
2018 年の秋以降、Windows に OpenSSH が追加され、Windows 10 と Windows Server 2019 に含まれています。

SSH は、ユーザーが操作しているシステムがクライアントであり、管理対象のリモート システムがサーバーである、クライアント/サーバー アーキテクチャに基づいています。
OpenSSH には、次のようなリモート システム管理に安全で簡単なアプローチを提供するように設計されたさまざまなコンポーネントとツールが含まれています。

* sshd.exe。リモートで管理されるシステム上で実行されている必要がある SSH サーバー コンポーネントです。
* ssh.exe: ユーザーのローカル システム上で実行される SSH クライアント コンポーネントです
* ssh-keygen.exe: SSH 用の認証キーを生成、管理、および変換します
* ssh-agent.exe: 公開キーの認証に使用される秘密キーを格納します
* ssh-add.exe: サーバーで許可される一覧に秘密キーを追加します
* ssh-keyscan.exe: 複数のホストから公開 SSH ホスト キーを収集するのに役立ちます
* sftp.exe: セキュア ファイル転送プロトコルを提供し、SSH 経由で実行されます
* scp.exe： SSH で実行されるファイル コピー ユーティリティです

このセクションのドキュメントでは、Windows での OpenSSH の使用方法 (インストール、Windows 固有の構成、およびユース ケースなど) を中心に説明します。 次のトピックがあります。

OpenSSH の一般的な 機能に関するその他の詳細なドキュメントについては、[OpenSSH.com](https://www.openssh.com/manual.html) でオンラインで確認できます。

マスター [OpenSSH オープン ソース プロジェクト](https://www.openssh.com) は、OpenBSD プロジェクトで開発者によって管理されています。
このプロジェクトの Microsoft フォークは [GitHub](https://github.com/PowerShell/openssh-portable) にあります。
Windows OpenSSH に関するフィードバックをお寄せください。[OpenSSH GitHub リポジトリ](https://github.com/PowerShell/openssh-portable)で GitHub Issue を作成することで提供できます。
