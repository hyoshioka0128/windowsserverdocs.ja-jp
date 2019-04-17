---
title: Server Core のインストール
description: 取得し、Windows Server 2019、Windows Server 2016、または Windows Server (半期チャネル) で Server Core インストールをインストールする方法。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 1/04/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d22818c-fbb7-487a-bb82-81ef0a3f7ede
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: d99cd0b028d08d5c3247541ce3a868676b60693d
ms.sourcegitcommit: 7fc7271745e40f110c54918b55624cadd0d7ff98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2019
ms.locfileid: "8991799"
---
# Server Core のインストール

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)
  
初めての Windows Server をインストールする場合は、次のインストール オプションがあります。

>[!NOTE]
> 次の一覧で、「デスクトップ エクスペリエンス」と記載されていないエディションが、Server Core インストール オプションです。

-   Windows Server Standard
-   Windows Server Standard (デスクトップ エクスペリエンスあり)
-   Windows Server Datacenter
-   Windows Server Datacenter (デスクトップ エクスペリエンスあり)

Windows Server (半期チャネル)、バージョン 1709、1803、1809 などをインストールする場合は、次のインストール オプションが必要。

-   Windows Server Standard 
-   Windows Server Datacenter

Server Core オプションでは、必要なディスク領域が減少し、攻撃を受ける可能性が低下しています。したがって、デスクトップ エクスペリエンス搭載サーバー オプションに含まれている追加的なユーザー インターフェイス要素やグラフィカル管理ツールを特に必要としなければ、Server Core インストールを選択することをお勧めします。 追加的なユーザー インターフェイス要素が必要な場合は、「[デスクトップ エクスペリエンスを使用したサーバーのインストール](Getting-Started-with-Server-with-Desktop-Experience.md)」をご覧ください。 

Server Core オプションでは、標準のユーザー インターフェイス (デスクトップ エクスペリエンス) はインストールされません。コマンド ラインや Windows PowerShell を使用するか、またはリモート操作でサーバーを管理します。

>[!NOTE]
>
>以前にリリースされた一部の Windows Server とは異なり、インストール後に、Server Core とデスクトップ エクスペリエンス搭載サーバーとの間の変換は実行できません。 Server Core をインストールし、後でデスクトップ エクスペリエンス搭載サーバーを使用することになった場合は、新規インストールを実行する必要があります。

**ユーザー インターフェイス:** コマンド プロンプト

**サーバーの役割をローカルにインストール、構成、アンインストール:** Windows PowerShell でコマンド プロンプトを使用。

**インストール、構成、Windows クライアント コンピューターからサーバーの役割をリモートでアンインストール (またはデスクトップ エクスペリエンス搭載サーバー インストール):** サーバー マネージャー、リモート サーバー管理ツール (RSAT)、Windows PowerShell、または Windows Admin Center にします。

>[!NOTE]
>
>RSAT の場合は、Windows 10 バージョンを使用する必要があります。
>Microsoft 管理コンソールは、ローカルでは使うことができません。

**例できるサーバーの役割:**

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
- ライセンス
- 仮想化
- ボリューム ライセンス認証サービス

Server Core に含まれていない役割、[役割、役割サービス、および Windows Server の Server Core ではなく機能](../administration/server-core/server-core-removed-roles.md)を参照してください。

## Windows Server 2019 または Windows Server 2016 にインストールします。

一般的なインストール手順と Windows Server (長期サービス チャネル) のオプションでは、 [Windows Server のインストールとアップグレード](installation-and-upgrade.md)を参照してください。

## Windows Server (半期チャネル) にインストールします。

Windows Server (半期チャネル) のインストールの手順は、以前のバージョンの Windows Server のインストールと同じ (から、します。ISO イメージの場合)、次の例外があります。
- 以前のバージョンの Windows Server から Windows Server バージョン 1709 へのアップグレードはサポートされていません。 常に新規インストールが必要です。
   これは、Windows コンピューターのデスクトップから setup.exe を実行すると、セットアップ エクスペリエンスを許可していません (、淡色)、アップグレード オプションを意味します。
- Windows Server (半期チャネル) の評価版はありません。
- OEM 版や製品版はありません。 Windows Server (半期チャネル) は、ソフトウェア アシュアランスまたはロイヤルティ プログラムを通じてのみライセンス供与することができます。

Windows Server バージョン 1709 を入手するには、「[Windows Server バージョン 1709 の概要](get-started-with-1709.md)」をご覧ください。

Windows Server バージョン 1803 を取得するのには、 [Windows Server の概要、バージョン 1803](get-started-with-1803.md)を参照してください。

新着 Windows Server version 1809 を参照してください[Windows Server version 1809 の新機能については](whats-new-in-windows-server-1809.md)
