---
title: 適切なインストールの種類
description: このトピックでは、Windows Admin Center のさまざまなインストール オプションについて説明します。これには、複数の管理者が使用する Windows 10 PC または Windows サーバーへのインストールが含まれます。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 12/02/2019
ms.openlocfilehash: bd7ec8a5a072cbda99b036718d24ec1908fb8b53
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269249"
---
# <a name="what-type-of-installation-is-right-for-you"></a>適切なインストールの種類

このトピックでは、Windows Admin Center のさまざまなインストール オプションについて説明します。これには、複数の管理者が使用する Windows 10 PC または Windows サーバーへのインストールが含まれます。 Azure にある VM 上に Windows Admin Center をインストールするには、「[Windows Admin Center を Azure にデプロイする](../azure/deploy-wac-in-azure.md)」を参照してください。

## <a name="installation-types"></a>インストール:種類

![img](../media/deployment-options/install-options.PNG)

| ローカル クライアント                                | ゲートウェイ サーバー                                  | マネージド サーバー                               | フェールオーバー クラスター                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| マネージド サーバーに接続されているローカルの Windows 10 クライアントに[インストール](../deploy/install.md)します。  クイック スタート、テスト、アドホックまたは小規模なシナリオに適しています。 |指定されたゲートウェイ サーバーに[インストール](../deploy/install.md)し、ゲートウェイ サーバーに接続している任意のクライアント ブラウザーからアクセスします。  大規模展開のシナリオに適しています。 | 自身を管理するため、またはメンバー ノードであるクラスターを管理するために、マネージド サーバーに直接[インストール](../deploy/install.md)します。  分散シナリオに適しています。 | ゲートウェイ サービスの高可用性を実現するために、フェールオーバー クラスターに[展開](#high-availability)します。 管理サービスの回復性を確保する運用環境に適しています。 |

## <a name="installation-supported-operating-systems"></a>インストール:サポートされているオペレーティング システム

Windows Admin Center は次の Windows オペレーティング システムに**インストール**することができます。

| **プラットフォーム**                       | **インストール モード** |
| -----------------------------------| --------------------- |
| Windows 10                         | ローカル クライアント |
| Windows Server 半期チャネル | ゲートウェイ サーバー、マネージド サーバー、フェールオーバー クラスター |
| Windows Server 2016                | ゲートウェイ サーバー、マネージド サーバー、フェールオーバー クラスター |
| Windows Server 2019                | ゲートウェイ サーバー、マネージド サーバー、フェールオーバー クラスター |

Windows Admin Center を操作するには:

- **ローカル クライアント シナリオ:** [Start]\(スタート\) メニューから Windows Admin Center ゲートウェイを起動し、`https://localhost:6516` にアクセスしてクライアント Web ブラウザーから接続します。
- **その他のシナリオ:** 別のコンピューター上の Windows Admin Center ゲートウェイにクライアント ブラウザーからその URL を使用して (たとえば、`https://servername.contoso.com`) 接続します。

> [!WARNING]
> ドメイン コントローラーへの Windows Admin Center のインストールはサポートされていません。 [ドメイン コントローラーのセキュリティに関するベスト プラクティスについて詳しくお読みください](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)。

## <a name="installation-supported-web-browsers"></a>インストール:サポートされている Web ブラウザー

Microsoft Edge ([Microsoft Edge インサイダー](https://microsoftedgeinsider.com)を含む) と Google Chrome がテストされ、Windows 10 でサポートされます。 他の Web ブラウザー (Internet Explorer および Firefox を含む) は、現在、弊社のテスト マトリックスには含まれていないため、"*正式には*" サポートされていません。 これらのブラウザーでは、Windows Admin Center の実行で問題が発生する可能性があります。 たとえば、Firefox には独自の証明書ストアがあるため、Windows 10 で Windows Admin Center を使用するには、`Windows Admin Center Client` 証明書を Firefox にインポートする必要があります。 詳細については、[ブラウザー固有の既知の問題](../support/known-issues.md#browser-specific-issues)に関するページを参照してください。

## <a name="management-target-supported-operating-systems"></a>管理の対象:サポートされているオペレーティング システム

Windows Admin Center を使って、次の Windows オペレーティング システムを**管理**することができます。

| バージョン | "*サーバー マネージャー*" を介した "*ノード*" の管理 | "*クラスターマネージャー*" を介した管理 |
| ------------------------- |--------------- | ----- |
| Windows 10 | はい (コンピューターの管理を使用) | なし |
| Windows Server 半期チャネル | はい | はい |
| Windows Server 2019 | はい | はい |
| Windows Server 2016 | はい | はい ([最新の累積的な更新プログラム](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center)を使用) |
| Microsoft Hyper-V Server 2016 | はい | はい |
| Windows Server 2012 R2 | はい | はい |
| Microsoft Hyper-V Server 2012 R2 | はい | はい |
| Windows Server 2012 | はい | はい |

> [!NOTE]
> Windows Admin Center では、Windows Server 2012 および 2012 R2 に含まれていない PowerShell 機能が必要です。 これらを Windows Admin Center で管理する場合は、Windows Management Framework (WMF) バージョン 5.1 以上をそれらのサーバーにインストールする必要があります。
> 
> PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。 
> 
> WMF がインストールされていない場合は、[WMF 5.1 をダウンロード](https://www.microsoft.com/download/details.aspx?id=54616)することができます。

## <a name="high-availability"></a>高可用性

フェールオーバー クラスター上のアクティブ/パッシブ モデルに Windows Admin Center を展開することにより、ゲートウェイ サービスの高可用性を実現できます。 クラスター内のいずれかのノードで障害が発生した場合、Windows Admin Center では別のノードに速やかにフェールオーバーされます。これにより、環境内のサーバーの管理をシームレスに進めることができます。

[Windows Admin Center の高可用性展開の方法をご確認ください](../deploy/high-availability.md)。

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)
