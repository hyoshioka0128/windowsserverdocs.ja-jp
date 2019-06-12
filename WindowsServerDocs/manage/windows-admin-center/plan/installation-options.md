---
title: インストールの種類が適切な
description: このトピックでは、複数の管理者によって、Windows 10 PC 上で使用するための Windows server のインストールを含む、Windows Admin Center のさまざまなインストール オプションについて説明します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 9b26ce28d8b3f74c26adab87e68b9985f2be5361
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811816"
---
# <a name="what-type-of-installation-is-right-for-you"></a>適切なインストールの種類

>適用先:Windows Admin Center、Windows Admin Center プレビュー

このトピックでは、複数の管理者によって、Windows 10 PC 上で使用するための Windows server のインストールを含む、Windows Admin Center のさまざまなインストール オプションについて説明します。 Azure 内の VM では、Windows Admin Center をインストールするを参照してください。 [Azure でデプロイ Windows Admin Center](../azure/deploy-wac-in-azure.md)します。

## <a name="supported-operating-systems-installation"></a>サポートされるオペレーティング システム:インストール

できます**インストール**次の Windows オペレーティング システムで Windows Admin Center:

| **バージョン**  | **インストール モード** |
| -------------| -----------------------|
| Windows 10 バージョン 1709 以降 | デスクトップ モード |
| Windows Server 半期チャネル | ゲートウェイ モード |
| Windows Server 2016 | ゲートウェイ モード |
| Windows Server 2019 | ゲートウェイ モード |

**デスクトップ モード:** [スタート] メニューから起動しがインストールされている同じコンピューターから Windows Admin Center ゲートウェイに接続する (つまり`https://localhost:6516`)

**ゲートウェイ モード:** 別のコンピューターにクライアントのブラウザーから、Windows Admin Center ゲートウェイに接続する (つまり`https://servername.contoso.com`) 

> [!WARNING]
> ドメイン コント ローラーで、Windows Admin Center をインストールすることはサポートされません。 [詳細については、ドメイン コント ローラーのセキュリティのベスト プラクティス](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)します。 

> [!IMPORTANT]
> Internet Explorer を使用して、Windows Admin Center を管理することはできません - 代わりに使用する必要があります、[サポートされているブラウザー](../understand/faq.md#which-web-browsers-are-supported-by-windows-admin-center
)します。  Windows Server を Windows Admin Center をインストールする Windows 10 とエッジをリモートで接続して管理することをお勧めします。  または、管理できますローカル Windows Server でサポートされているブラウザーをインストールしている場合。

## <a name="supported-operating-systems-management"></a>サポートされるオペレーティング システム:管理

できます**管理**Windows Admin Center を使用して、次の Windows オペレーティング システム。

| バージョン | 管理*ノード*を介して*サーバー マネージャー* | 管理*クラスター*を介して*フェールオーバー クラスター マネージャー* | 管理*HCI*を介して*HCI クラスター マネージャー* |
| ------------------------- |--------------- | ----- | ------------------------ |
| Windows 10 バージョン 1709 以降 | [はい] (コンピューターの管理) 経由 | なし | なし |
| Windows Server 半期チャネル | 〇 | 〇 | なし |
| Windows Server 2019 | 〇 | 〇 | 〇 |
| Windows Server 2016 | 〇 | 〇 | Yes, with[最新の累積的な更新プログラム](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | 〇 | 〇 | なし |
| Windows Server 2012 R2 | 〇 | 〇 | なし |
| Microsoft Hyper-V Server 2012 R2 | 〇 | 〇 | なし |
| Windows Server 2012 | 〇 | 〇 | なし |
| Windows Server 2008 R2 | はい、機能制限 | なし | なし |

> [!NOTE]
> Windows Admin Center では、PowerShell の機能は、Windows Server 2008 R2、2012、および 2012 R2 には含まれていない必要があります。 Windows Admin Center で管理する場合、これらのサーバーで Windows Management Framework (WMF) 5.1 以降のバージョンをインストールする必要があります。
> 
> PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。 
> 
> WMF がインストールされていない場合は、 [WMF 5.1 のダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=54616)します。

## <a name="deployment-options"></a>展開オプション

| ![img](../media/deployment-options/W10.png) | ![img](../media/deployment-options/gateway.png) | ![img](../media/deployment-options/node.png) | ![img](../media/deployment-options/HA.png) |
| --------------------------------------------- | ------------------------------------------------- |----------------------------------------------|-------------------------------------------- |
|                                             |                                                 |                                              |                                            |

| ローカル クライアント | ゲートウェイ サーバー | 管理されたサーバー | フェールオーバー クラスター |
| --- | --- | --- | --- |
| 管理対象サーバーに接続されているローカルの Windows 10 クライアントをインストールします。  クイック スタートで、テスト、アドホックまたは小規模なシナリオに適しています。 |指定されたゲートウェイ サーバーをインストールし、ゲートウェイ サーバーへの接続に任意のクライアント ブラウザーからアクセスします。  大規模なシナリオに適しています。 | それ自体またはメンバー ノードがクラスターを管理するための管理対象サーバーに直接インストールします。  分散のシナリオに適しています。 | ゲートウェイ サービスの高可用性を有効にするフェールオーバー クラスターにデプロイします。 管理サービスの回復性を確実に運用環境に適しています。 |

## <a name="high-availability"></a>高可用性

フェールオーバー クラスター上のアクティブ/パッシブ モデルで Windows Admin Center を展開することで、ゲートウェイ サービスの高可用性を有効にできます。 クラスター内のノードのいずれかが失敗した場合は場合、Windows Admin Center 適切にフェールオーバー操作が別のノードに引き続きシームレスに環境内のサーバーを管理することができます。

[高可用性を備えた Windows Admin Center を展開する方法について説明します。](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)
