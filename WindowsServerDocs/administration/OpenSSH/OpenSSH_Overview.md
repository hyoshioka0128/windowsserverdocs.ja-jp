---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendmsft
title: Windows での OpenSSH
ms.product: windows-server
ms.openlocfilehash: 57126f38245f4547a04ea3a51f58aee865b5eb97
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852035"
---
# <a name="openssh-in-windows"></a>Windows での OpenSSH

OpenSSH は、Linux と非 Windows の管理者が、リモート システムのクロスプラットフォーム管理を行うために使用するオープンソース バージョンの Secure Shell (SSH) ツールです。 2018 年の秋以降、Windows に OpenSSH が追加され、Windows 10 と Windows Server 2019 に含まれています。 

SSH は、ユーザーが操作しているシステムがクライアントであり、管理対象のリモート システムがサーバーである、クライアント/サーバー アーキテクチャに基づいています。 OpenSSH には、次のようなリモート システム管理に安全で簡単なアプローチを提供するように設計されたさまざまなコンポーネントとツールが含まれています。

* sshd.exe。リモートで管理されるシステム上で実行されている必要がある SSH サーバー コンポーネントです。 
* ssh.exe: ユーザーのローカル システム上で実行される SSH クライアント コンポーネントです
* ssh-keygen.exe: SSH 用の認証キーを生成、管理、および変換します 
* ssh-agent.exe: 公開キーの認証に使用される秘密キーを格納します
* ssh-add.exe: サーバーで許可される一覧に秘密キーを追加します
* ssh-keyscan.exe: 複数のホストから公開 SSH ホスト キーを収集するのに役立ちます
* sftp.exe: セキュア ファイル転送プロトコルを提供し、SSH 経由で実行されます
* scp.exe： SSH で実行されるファイル コピー ユーティリティです

このセクションのドキュメントでは、Windows での OpenSSH の使用方法 (インストール、Windows 固有の構成、およびユース ケースなど) を中心に説明します。 次のトピックがあります。
* Windows Server 2019 および Windows 10 用 OpenSSH のインストールとアンインストール

OpenSSH の一般的な 機能に関するその他の詳細なドキュメントについては、[OpenSSH.com](https://www.openssh.com/manual.html) でオンラインで確認できます。 

マスター [OpenSSH オープン ソース プロジェクト](https://www.openssh.com) は、OpenBSD プロジェクトで開発者によって管理されています。 このプロジェクトの Microsoft フォークは [GitHub](https://github.com/PowerShell/openssh-portable) にあります。
Windows OpenSSH に関するフィードバックをお寄せください。[OpenSSH GitHub リポジトリ](https://github.com/PowerShell/openssh-portable)で GitHub Issue を作成することで提供できます。 
