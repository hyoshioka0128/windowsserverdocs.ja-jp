---
title: Server Core のインストール
description: コア インストールを取得して、Windows Server 2019、Windows Server 2016 または Windows Server (半期チャネル) にインストールする方法。
ms.prod: windows-server-threshold
ms.date: 05/21/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 6f685ce29088b56bb243d21315787ab90e6863a4
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "65976718"
---
# <a name="install-server-core"></a>Server Core のインストール

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)
  
初めて Windows Server をインストールする場合は、次のインストール オプションがあります。

>[!NOTE]
> 次の一覧で、「デスクトップ エクスペリエンス」と記載されていないエディションが、Server Core インストール オプションです。

-   Windows Server Standard
-   Windows Server Standard (デスクトップ エクスペリエンスあり)
-   Windows Server Datacenter
-   Windows Server Datacenter (デスクトップ エクスペリエンスあり)

初めて Windows Server (半期チャネル) をインストールする場合は、次のインストール オプションがあります。

-   Windows Server Standard 
-   Windows Server Datacenter

Server Core オプションでは、必要なディスク領域が減少し、攻撃を受ける可能性が低下しています。したがって、デスクトップ エクスペリエンス搭載サーバー オプションに含まれている追加的なユーザー インターフェイス要素やグラフィカル管理ツールを特に必要としなければ、Server Core インストールを選択することをお勧めします。 追加的なユーザー インターフェイス要素が必要な場合は、「[デスクトップ エクスペリエンスを使用したサーバーのインストール](Getting-Started-with-Server-with-Desktop-Experience.md)」をご覧ください。 

Server Core オプションでは、標準のユーザー インターフェイス (デスクトップ エクスペリエンス) はインストールされません。コマンド ラインや Windows PowerShell を使用するか、またはリモート操作でサーバーを管理します。

>[!NOTE]
>
>以前にリリースされた一部の Windows Server とは異なり、インストール後に、Server Core とデスクトップ エクスペリエンス搭載サーバーとの間の変換は実行できません。 Server Core をインストールし、後でデスクトップ エクスペリエンス搭載サーバーを使用することになった場合は、新規インストールを実行する必要があります。

**ユーザー インターフェイス:** コマンド プロンプト

**サーバーの役割をローカルにインストール、構成、アンインストール:** Windows PowerShell でコマンド プロンプトを使用。

**サーバーの役割を Windows クライアント コンピューター (またはデスクトップ エクスペリエンスがインストールされたサーバー) からリモートでインストール、構成、アンインストール:** サーバー マネージャー、リモート サーバー管理ツール (RSAT)、Windows PowerShell、または Windows Admin Center を使用。

>[!NOTE]
>
>RSAT の場合は、Windows 10 バージョンを使用する必要があります。
>Microsoft 管理コンソールは、ローカルでは使うことができません。

**使用できるサーバーの役割の例:**

- Active Directory 証明書サービス
- [Active Directory Domain Services]
- DHCP サーバー
- DNS サーバー
- ファイル サーバー (ファイル サーバー リソース マネージャーを含む)
- Active Directory ライトウェイト ディレクトリ サービス (AD LDS)
- Hyper-V
- 印刷とドキュメント サービス
- ストリーミング メディア サービス
- Web サーバー (ASP.NET のサブセットを含む)
- Windows Server Update Server
- Active Directory Rights Management サーバー
- ルーティングとリモート アクセス サーバーおよび次のサブ役割:
   - リモート デスクトップ サービス接続ブローカー
   - Licensing
   - 仮想化
   - ボリューム ライセンス認証サービス

Server Core に含まれていない役割については、「[Windows Server - Server Core に含まれていない役割、役割サービス、および機能](../administration/server-core/server-core-removed-roles.md)」を参照してください。

## <a name="installing-on-windows-server-2019-or-windows-server-2016"></a>Windows Server 2019 または Windows Server 2016 のインストール

Windows Server (長期サービス チャネル) の一般的なインストール手順とオプションについては、「[Windows Server のインストールとアップグレード](installation-and-upgrade.md)」を参照してください。

## <a name="installing-on-windows-server-semi-annual-channel"></a>Windows Server (半期チャネル) のインストール

Windows Server (半期チャネル) のインストールの手順は、以前のバージョンの Windows Server のインストールと同じ (.ISO イメージからの場合) ですが、次のような例外があります。

- 以前のバージョンの Windows Server から Windows Server バージョン 1709 へのアップグレードはサポートされていません。 常に新規インストールが必要です。
   これは、Windows コンピューターのデスクトップから setup.exe を実行する場合、セットアップ エクスペリエンスでアップグレード オプションが許可されない (灰色表示される) ことを意味します。
- Windows Server (半期チャネル) の評価版はありません。
- OEM 版や製品版はありません。 Windows Server (半期チャネル) は、ソフトウェア アシュアランスまたはロイヤルティ プログラムを通じてのみライセンス供与されます。

半期チャネルの詳細については、「[サービス チャネルの比較](../get-started-19/servicing-channels-19.md)」を参照してください。

Windows Server 半期チャネルの新機能については、「[Windows Server の新機能](whats-new-in-windows-server.md)」を参照してください。
