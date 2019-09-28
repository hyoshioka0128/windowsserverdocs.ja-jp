---
title: 適切なインストールの種類
description: このトピックでは、windows 管理センターのさまざまなインストールオプションについて説明します。これには、複数の管理者が使用する windows 10 PC または Windows server へのインストールが含まれます。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: 144c57bba621ee1b94a66914f8d9b6c0292f8b03
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406872"
---
# <a name="what-type-of-installation-is-right-for-you"></a>適切なインストールの種類

>適用先:Windows Admin Center、Windows Admin Center Preview

このトピックでは、windows 管理センターのさまざまなインストールオプションについて説明します。これには、複数の管理者が使用する windows 10 PC または Windows server へのインストールが含まれます。 Azure の VM に Windows 管理センターをインストールする方法については、「 [azure での Windows 管理センターのデプロイ](../azure/deploy-wac-in-azure.md)」を参照してください。

## <a name="installation-types"></a>インストール:種類

| ローカルクライアント                                | ゲートウェイ サーバー                                  | 管理対象サーバー                               | フェールオーバー クラスター                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| ![img](../media/deployment-options/W10.PNG) | ![img](../media/deployment-options/gateway.PNG) | ![img](../media/deployment-options/node.PNG) | ![img](../media/deployment-options/HA.png) |
| 管理対象サーバーに接続できるローカルの Windows 10 クライアントにをインストールします。  クイックスタート、テスト、アドホックまたは小規模なシナリオに適しています。 |指定したゲートウェイサーバーにをインストールし、ゲートウェイサーバーに接続されている任意のクライアントブラウザーからアクセスします。  大規模なシナリオに適しています。 | 自身またはメンバーノードであるクラスターを管理するために、管理対象サーバーに直接インストールします。  分散型のシナリオに適しています。 | ゲートウェイサービスの高可用性を実現するには、をフェールオーバークラスターに展開します。 運用環境では、管理サービスの回復性を確保するために適しています。 |

## <a name="installation-supported-operating-systems"></a>インストール:サポートされるオペレーティング システム

Windows 管理センターは、次の Windows オペレーティングシステムに**インストール**できます。

| **プラットフォーム**                       | **インストールモード** |
| -----------------------------------| --------------------- |
| Windows 10 バージョン1709以降  | ローカルクライアント |
| Windows Server 半期チャネル | ゲートウェイサーバー、管理サーバー、フェールオーバークラスター |
| Windows Server 2016                | ゲートウェイサーバー、管理サーバー、フェールオーバークラスター |
| Windows Server 2019                | ゲートウェイサーバー、管理サーバー、フェールオーバークラスター |

Windows 管理センターを操作するには:

- **ローカルクライアントのシナリオの場合:** [スタート] メニューから Windows 管理センターゲートウェイを起動し、`https://localhost:6516` にアクセスしてクライアント web ブラウザーから接続します。
- **その他のシナリオの場合:** URL (たとえば、`https://servername.contoso.com`) を使用して、クライアントブラウザーから別のコンピューターの Windows 管理センターゲートウェイに接続します。

> [!WARNING]
> ドメインコントローラーへの Windows 管理センターのインストールはサポートされていません。 [詳細については、「ドメインコントローラーのセキュリティに関するベストプラクティス](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack)」を参照してください。 

## <a name="installation-supported-web-browsers"></a>インストール:サポートされている web ブラウザー

Microsoft Edge と Google Chrome は、Windows 10 でテストおよびサポートされています。 Internet Explorer や Firefox などの他の web ブラウザーは、現在テストマトリックスの一部ではないため、*公式*にはサポートされていません。 これらのブラウザーでは、Windows 管理センターの実行に問題がある可能性があります。 たとえば、Firefox には独自の証明書ストアがあるため、Windows 10 で Windows 管理センターを使用するには `Windows Admin Center Client` 証明書を Firefox にインポートする必要があります。 詳細については、「[ブラウザー固有の既知の問題](../support/known-issues.md#browser-specific-issues)」を参照してください。

## <a name="management-target-supported-operating-systems"></a>管理対象:サポートされるオペレーティング システム

Windows 管理センターを使用して、次の Windows オペレーティングシステムを**管理**できます。

| バージョン | *サーバーマネージャー*を使用した*ノード*の管理 | *フェールオーバークラスターマネージャー*を使用した*クラスター*の管理 | *HCI クラスターマネージャー*を使用して*HCI*を管理する |
| ------------------------- |--------------- | ----- | ------------------------ |
| Windows 10 バージョン1709以降 | はい (コンピューターの管理を使用) | なし | なし |
| Windows Server 半期チャネル | はい | 〇 | なし |
| Windows Server 2019 | はい | [はい] | はい |
| Windows Server 2016 | はい | はい | はい ([最新の累積的な更新プログラム](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center)あり) |
| Microsoft Hyper-V Server 2016 | はい | 〇 | なし |
| Windows Server 2012 R2 | はい | 〇 | なし |
| Microsoft Hyper-V Server 2012 R2 | はい | 〇 | なし |
| Windows Server 2012 | はい | 〇 | なし |
| Windows Server 2008 R2 | はい (制限された機能) | なし | なし |

> [!NOTE]
> Windows 管理センターには、Windows Server 2008 R2、2012、および 2012 R2 に含まれていない PowerShell 機能が必要です。 Windows 管理センターで管理する場合は、これらのサーバーに Windows Management Framework (WMF) バージョン5.1 以降をインストールする必要があります。
> 
> PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。 
> 
> WMF がインストールされていない場合は、 [wmf 5.1 をダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=54616)できます。

## <a name="high-availability"></a>高可用性

フェールオーバークラスターのアクティブ/パッシブモデルに Windows 管理センターを展開することにより、ゲートウェイサービスの高可用性を有効にすることができます。 クラスター内のいずれかのノードで障害が発生した場合、Windows 管理センターは正常に別のノードにフェールオーバーします。これにより、環境内のサーバーの管理をシームレスに進めることができます。

[高可用性を備えた Windows 管理センターを展開する方法について説明します。](../deploy/high-availability.md)

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)
