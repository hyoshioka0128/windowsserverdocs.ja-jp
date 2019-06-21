---
ms.date: 01/07/2019
contributor: damaerteMSFT
author: maertendMSFT
keywords: OpenSSH を SSH での Win32 OpenSSH
title: Windows で OpenSSH
ms.product: w10
ms.openlocfilehash: c6563fbe4fe69acad4d295a3f7fe166e92d38444
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280057"
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

マスター [OpenSSH オープン ソース プロジェクト](https://www.openssh.com)OpenBSD プロジェクトの開発者によって管理されます。 このプロジェクトの Microsoft のフォークが[GitHub](https://github.com/PowerShell/openssh-portable)します。
Windows OpenSSH に関するフィードバックのことし、で GitHub の issue を作成して指定することができます、 [OpenSSH GitHub リポジトリ](https://github.com/PowerShell/openssh-portable)します。 
