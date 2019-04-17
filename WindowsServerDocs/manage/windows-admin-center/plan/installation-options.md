---
title: インストールの種類に適切な
description: このトピックでは、Windows Admin Center に複数の管理者によって、Windows 10 PC に使用するための Windows server のインストールなどのさまざまなインストール オプションについて説明します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: cc6f9e6c2f2572618c1c5fdae00047d24fbeb3cf
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296664"
---
# 適切なインストールの種類

>適用対象: Windows Admin Center、Windows Admin Center Preview

このトピックでは、Windows Admin Center に複数の管理者によって、Windows 10 PC に使用するための Windows server のインストールなどのさまざまなインストール オプションについて説明します。 Azure で VM に Windows Admin Center をインストールするには、 [Azure で Windows Admin Center を展開](../azure/deploy-wac-in-azure.md)を参照してください。

## サポートされているオペレーティング システム: インストール

次の Windows オペレーティング システムで Windows Admin Center を**インストール**を実行できます。

| **バージョン** | **インストール モード** |
|-------------|-----------------------|
|Windows 10 バージョン 1709 以降 | デスクトップ モード |
|Windows Server 半期チャネル | ゲートウェイ モード |
|Windows Server 2016 | ゲートウェイ モード |
|Windows Server 2019 | ゲートウェイ モード |

**デスクトップ モード:**[スタート] メニューから起動し、それがインストールされている同じコンピューターから Windows Admin Center ゲートウェイに接続 (つまり`https://localhost:6516`)

**ゲートウェイ モード:** 別のコンピューター上のクライアント ブラウザーから Windows Admin Center ゲートウェイに接続 (つまり`https://servername.contoso.com`) 

> [!WARNING]
> ドメイン コント ローラーで Windows Admin Center をインストールすることはサポートされていません。 [ドメイン コント ローラーのセキュリティのベスト プラクティスについて確認してください](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)。 

> [!IMPORTANT]
> Internet Explorer を使って Windows Admin Center を管理することはできません - 代わりに、[ブラウザーのサポート](../understand/faq.md#which-web-browsers-are-supported-by-windows-admin-center
)を使用する必要があります。  Windows Server で Windows Admin Center をインストールする場合は、Windows 10 と Edge リモートで接続して管理することをお勧めします。  または、管理できますローカル Windows Server でサポートされているブラウザーをインストールした場合。

## サポートされているオペレーティング システム: 管理

できます**管理**Windows Admin Center を使用して次の Windows オペレーティング システム。

| バージョン | *サーバー マネージャー*を使用して、*ノードを*管理します。 | *フェールオーバー クラスター マネージャー*を使用して*クラスターを*管理します。 | 管理*HCI クラスター マネージャー*を使用して*HCI*|
|-------------------------|---------------|-----|------------------------|
| Windows 10 バージョン 1709 以降 | [はい] (コンピューターの管理) を介して | なし | なし |
| Windows Server 半期チャネル | はい | ○ | なし |
| Windows Server 2019 | はい | はい | 要 |
| Windows Server 2016 | はい | はい | はい、[最新の累積的な更新プログラム](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | はい | ○ | なし |
| Windows Server 2012 R2 | はい | ○ | なし |
| Microsoft Hyper-V Server 2012 R2 | はい | ○ | なし |
| Windows Server 2012 | 可 | ○ | なし |
| Windows Server 2008 R2 | はい、制限された機能 | なし | なし |

> [!NOTE]
> Windows Admin Center には、Windows Server 2008 R2、2012 および 2012 R2 に含まれていない PowerShell 機能が必要です。 Windows Admin Center でこれらを管理する場合は、それらのサーバーに Windows Management Framework (WMF) バージョン 5.1 以上をインストールする必要があります。

>PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。 

>WMF がインストールされていない場合は、 [WMF 5.1 をダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=54616)できます。

## 展開オプション

| ![img](../media/deployment-options/W10.png) | ![img](../media/deployment-options/gateway.png) | ![img](../media/deployment-options/node.png) | ![img](../media/deployment-options/HA.png) |
|---|---|---|---|

| ローカル クライアント | ゲートウェイ サーバー | 管理対象サーバー | フェールオーバー クラスター |
| --- | --- | --- | --- |
| 管理対象サーバーへの接続しているローカルの Windows 10 クライアントをインストールします。  クイック スタート、テスト、アドホックまたは小規模なシナリオに最適です。 |指定されたゲートウェイ サーバーをインストールし、ゲートウェイ サーバーに接続された任意のクライアント ブラウザーからアクセスします。  大規模なシナリオに便利です。 | 自体またはメンバー ノードがクラスターを管理するための管理対象サーバーに直接インストールします。  分散シナリオに便利です。 | ゲートウェイ サービスの可用性を有効にするには、フェールオーバー クラスターを展開します。 運用環境の管理サービスの回復性を確認する便利です。 |

## 高可用性

フェールオーバー クラスターでアクティブ パッシブ モデルでは、Windows Admin Center を展開することによって、ゲートウェイ サービスの可用性を有効にできます。 クラスター内のノードのいずれかが失敗した場合は、Windows Admin Center 適切フェールオーバー別のノードに引き続きシームレスに環境内のサーバーを管理すること。

[高可用性を Windows Admin Center を展開する方法について説明します。](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)
