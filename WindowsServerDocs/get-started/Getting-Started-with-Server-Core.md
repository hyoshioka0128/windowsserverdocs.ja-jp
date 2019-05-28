---
title: Server Core のインストール
description: 取得して、Windows Server 2019、Windows Server 2016 または Windows Server (半期チャネル) の Server Core インストールをインストールする方法。
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
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976718"
---
# <a name="install-server-core"></a>Server Core のインストール

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)
  
初めての Windows Server をインストールするときに、次のインストール オプションがあります。

>[!NOTE]
> 次の一覧で、「デスクトップ エクスペリエンス」と記載されていないエディションが、Server Core インストール オプションです。

-   Windows Server Standard
-   Windows Server Standard (デスクトップ エクスペリエンスあり)
-   Windows Server Datacenter
-   Windows Server Datacenter (デスクトップ エクスペリエンスあり)

Windows Server (半期チャネル) をインストールするときに、次のインストール オプションがあります。

-   Windows Server Standard 
-   Windows Server Datacenter

Server Core オプションでは、必要なディスク領域が減少し、攻撃を受ける可能性が低下しています。したがって、デスクトップ エクスペリエンス搭載サーバー オプションに含まれている追加的なユーザー インターフェイス要素やグラフィカル管理ツールを特に必要としなければ、Server Core インストールを選択することをお勧めします。 追加的なユーザー インターフェイス要素が必要な場合は、「[デスクトップ エクスペリエンスを使用したサーバーのインストール](Getting-Started-with-Server-with-Desktop-Experience.md)」をご覧ください。 

Server Core オプションでは、標準のユーザー インターフェイス (デスクトップ エクスペリエンス) はインストールされません。コマンド ラインや Windows PowerShell を使用するか、またはリモート操作でサーバーを管理します。

>[!NOTE]
>
>以前にリリースされた一部の Windows Server とは異なり、インストール後に、Server Core とデスクトップ エクスペリエンス搭載サーバーとの間の変換は実行できません。 Server Core をインストールし、後でデスクトップ エクスペリエンス搭載サーバーを使用することになった場合は、新規インストールを実行する必要があります。

**ユーザー インターフェイス:** コマンド プロンプト

**サーバーの役割をローカルにインストール、構成、アンインストール:** Windows PowerShell でコマンド プロンプトを使用。

**インストール、構成、Windows クライアント コンピューター (またはインストールされているデスクトップ エクスペリエンス搭載サーバー) からサーバーの役割をリモート アンインストール:** サーバー マネージャー、リモート サーバー管理ツール (RSAT)、Windows PowerShell、または Windows Admin Center.

>[!NOTE]
>
>RSAT の場合は、Windows 10 バージョンを使用する必要があります。
>Microsoft 管理コンソールは、ローカルでは使うことができません。

**使用できる例サーバー ロール:**

- Active Directory 証明書サービス
- Active Directory Domain Services
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

ロールの Server Core に含まれていない場合、次を参照してください。[役割、役割サービス、および Windows Server の Server Core ではなく機能](../administration/server-core/server-core-removed-roles.md)します。

## <a name="installing-on-windows-server-2019-or-windows-server-2016"></a>Windows Server 2019 または Windows Server 2016 にインストールします。

一般的なインストール手順と Windows Server (時間の長い用語サービス チャネル) のオプションは、次を参照してください。 [Windows Server のインストールとアップグレード](installation-and-upgrade.md)します。

## <a name="installing-on-windows-server-semi-annual-channel"></a>Windows Server (半期チャネル) へのインストール

Windows Server (半期チャネル) のインストール手順は、旧バージョンの Windows Server のインストールと同じ (から、します。ISO イメージの場合)、次の例外。

- 以前のバージョンの Windows Server から Windows Server バージョン 1709 へのアップグレードはサポートされていません。 常に新規インストールが必要です。
   これは、Windows コンピューターのデスクトップから setup.exe を実行すると、セットアップ エクスペリエンスは許可されていないこと (淡色) アップグレード オプションを意味します。
- Windows Server (半期チャネル) の評価版ではありません。
- OEM 版や製品版はありません。 Windows Server (半期チャネル) は、ソフトウェア アシュアランスやロイヤルティ プログラムを通してのみライセンスことができます。

半期チャネルの詳細については、次を参照してください。[サービス チャネルの比較](../get-started-19/servicing-channels-19.md)します。

新機能については Windows Server 半期チャネルを表示するを参照してください[Windows Server では新機能。](whats-new-in-windows-server.md)
