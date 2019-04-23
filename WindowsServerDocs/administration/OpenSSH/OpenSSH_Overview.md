---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH を SSH での Win32 OpenSSH
title: Windows で OpenSSH
ms.product: w10
ms.openlocfilehash: 68ced1ff133495d7658e486e7e72321e18857b21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843363"
---
# <a name="openssh-in-windows"></a>Windows で OpenSSH

OpenSSH は、Linux の管理者およびその他の非 Windows リモート システムのクロス プラットフォームの管理に使用する Secure Shell (SSH) ツールのオープン ソース バージョンです。 OpenSSH は、2018 年の秋の時点で Windows に追加されたおよび Windows 10 および Windows Server 2019 が含まれます。 

SSH は、クライアント サーバー アーキテクチャ、ユーザーが使用システムがクライアントであり、管理されているリモート システムがサーバーに基づきます。 OpenSSH には、さまざまなコンポーネントをリモート システムの管理のセキュリティで保護された、簡単なアプローチを提供するよう設計されたツールが含まれています。 など。

* これは、リモートで管理されているシステムで実行する必要がある SSH サーバー コンポーネント、sshd.exe 
* これは、ユーザーのローカル システムで実行されている SSH クライアント コンポーネント、ssh.exe
* ssh-keygen.exe は、生成され、管理の SSH 認証キーに変換します 
* ssh-agent.exe 公開キー認証に使用される秘密キーを格納します。
* ssh-add.exe は、秘密キーをサーバーで許可されている、一覧に追加されます。
* ssh-keyscan.exe ホストの数からの SSH の公開ホスト キーの収集を支援
* sftp.exe は、セキュリティで保護されたファイル転送プロトコルを提供し、SSH 経由で実行されるサービスです。
* scp.exe が SSH で実行されているファイルのコピー ユーティリティです。

このセクションでは、OpenSSH をインストール、および Windows に固有の構成と使用例を含む、Windows で使用する方法について説明します。 トピックでは、次に示します。
* インストールと Windows Server 2019 および Windows 10 の OpenSSH をアンインストールします。

OpenSSH の一般的な機能の追加の詳細なドキュメントはオンラインで[OpenSSH.com](https://www.openssh.com/manual.html)します。 

マスター [OpenSSH オープン ソース プロジェクト](https://www.openssh.com)OpenBSD プロジェクトの開発者によって管理されます。 このプロジェクトの Microsoft のフォークが[Github](https://github.com/PowerShell/openssh-portable)します。
Windows OpenSSH に関するフィードバックのことし、で Github の issue を作成して指定することができます、 [OpenSSH Github リポジトリ](https://github.com/PowerShell/openssh-portable)します。 
