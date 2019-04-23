---
title: デスクトップ ホスティングの Azure サービスと考慮事項
description: リモートのデスクトップ ホスティング ソリューションを Azure に固有の考慮事項について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f402ae3-5391-4c7d-afea-2c5c9044de46
author: heidilohr
manager: dougkim
ms.openlocfilehash: 37210a5d75399309c53364f5b8ee9e06d26d6f32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849803"
---
# <a name="azure-services-and-considerations-for-desktop-hosting"></a>デスクトップ ホスティングの Azure サービスと考慮事項

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

次のセクションでは、Azure インフラストラクチャ サービスについて説明します。
  
## <a name="azure-portal"></a>Azure portal

プロバイダーは、Azure サブスクリプションで作成された後、各テナントの環境を手動で作成する、Azure portal を使用できます。 PowerShell スクリプトを使用してこのプロセスを自動化することもできます。  

詳細については、次を参照してください。、 [Microsoft Azure](https://www.azure.microsoft.com) web サイト。
  
## <a name="azure-load-balancer"></a>Azure Load Balancer

テナントのコンポーネントでは、分離されたネットワークで相互通信する仮想マシンで実行します。 展開プロセス中、これらの仮想マシンをリモート デスクトップ プロトコル エンドポイントまたはリモート PowerShell エンドポイントを使用して Azure Load Balancer 経由外部からアクセスできます。 デプロイが完了すると、攻撃対象領域を削減する通常これらのエンドポイントが削除されます。 唯一のエンドポイントは、RD Web と RD ゲートウェイ コンポーネントを実行する仮想マシンの作成と UDP の HTTPS エンドポイントになります。 これにより、クライアントは、インターネット、テナントのデスクトップ ホスティング サービスで実行されているセッションに接続するためにします。 ユーザーが web ブラウザーなど、インターネットに接続しているアプリケーションを開いた場合、Azure Load Balancer 経由の接続が渡されます。  
  
詳細については、次を参照してください[Azure Load Balancer とは何ですか?。](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-load-balance/)
  
## <a name="security-considerations"></a>セキュリティの考慮事項

この Azure デスクトップ ホスティング参照アーキテクチャ ガイドは、各テナントに対して高い安全性と分離された環境を提供する設計されています。 システムのセキュリティは、ホステッド サービスの展開と操作中に、プロバイダーが行うセーフガードによっても異なります。 次の一覧には、セキュリティで保護されたこの参照アーキテクチャに基づき、デスクトップ ホスティング ソリューションを保持する、プロバイダーが実行するいくつかの考慮事項について説明します。

- すべての管理パスワードは、理想的にはランダムに生成された、頻繁に変更され、選択のいくつかプロバイダー管理者のみアクセスできるようにセキュリティで保護された中央の場所に保存、強力なである必要があります。  
- 新しいテナントのテナント環境をレプリケートするときに、同じまたは脆弱な管理者のパスワードを使用しないでください。
- RD Web アクセス サイトの URL、名、および証明書は、一意であり、スプーフィング攻撃を防止するには、各テナントに認識できるものにある必要があります。  
- デスクトップ ホスティング サービスの通常の操作には、ユーザーがテナントのデスクトップ ホスティング クラウド サービスに安全に接続できるように、RD Web と RD ゲートウェイ仮想マシンを除くすべての仮想マシンのすべてのパブリック IP アドレスを削除してください。 管理タスクに必要な場合、パブリック IP アドレスを一時的に追加することがありますが、後で削除するか常にします。  
  
詳しくは、次の記事をご覧ください。

- [セキュリティと保護](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831778(v=ws.11))  
- [IIS 8 のセキュリティのベスト プラクティス](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj635855(v=ws.11))  
- [Windows Server 2012 R2 をセキュリティで保護します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831360(v=ws.11))  
  
## <a name="design-considerations"></a>設計時の考慮事項

マルチ テナントのデスクトップ ホスティング サービスを設計するときに、Microsoft Azure インフラストラクチャ サービスの制約を検討してください。 次の一覧には、機能とコスト効果の高いデスクトップ ホスティングに基づいてソリューションをこの参照アーキテクチャを実現するために、プロバイダーを実行する必要がありますの考慮事項について説明します。  
  
- Azure サブスクリプションには仮想ネットワーク、VM コア、および使用できるクラウド サービスの最大数。 プロバイダーは、これより多くのリソースを必要とする場合は、複数のサブスクリプションを作成する必要があります。
- Azure クラウド サービスが、使用できる仮想マシンの最大数。 プロバイダーは、複数のクラウド サービスの最大数を超える大規模なテナントを作成する必要があります。  
- Azure の展開のコストは、仮想マシンのサイズと数に部分的に基づいています。 プロバイダーは、数と各テナント用の仮想マシンのサイズ、機能を提供し、安全性の高い低いコストでデスクトップ ホスティング環境を最適化する必要があります。  
- Azure データ センターの物理コンピューターのリソースは、HYPER-V を使用して仮想化されます。 仮想マシンの可用性は、Azure インフラストラクチャで使用される個々 のサーバーの可用性に依存しているために、ホスト クラスターで HYPER-V ホストは構成されていません。 高可用性を提供するには、仮想マシン内でのゲスト クラスタ リングを実装することができますしに各役割サービスの仮想マシンの複数のインスタンスを可用性セットに作成できます。  
- 一般的なストレージ構成では、サービス プロバイダーは (たとえば、1 つ、各テナントに対して)、複数のコンテナーと各コンテナー内で複数のディスクを 1 つのストレージ アカウントになります。 ただし、記憶域の合計と 1 つのストレージ アカウントで達成できるパフォーマンスに制限があります。 多数のテナントまたはテナントの高いストレージ容量またはパフォーマンスの要件をサポートするサービス プロバイダー、サービス プロバイダーは、複数のストレージ アカウントを作成する必要があります。  
  
詳しくは、次の記事をご覧ください。

- [Cloud Services のサイズ](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs)  
- [Microsoft Azure 仮想マシンの料金詳細](https://azure.microsoft.com/pricing/details/virtual-machines/)  
- [HYPER-V の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11))  
- [Azure Storage のスケーラビリティとパフォーマンスのターゲット](https://docs.microsoft.com/azure/storage/common/storage-scalability-targets)  

## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory アプリケーション プロキシ

Azure Active Directory (AD) アプリケーション プロキシは、有料 Sku の Azure AD ユーザーが Azure のリバース プロキシ サービス経由で内部アプリケーションに接続できるで提供されるサービスです。 これにより、パブリック IP アドレスでインターネットに公開する必要がないため、仮想ネットワーク内で非表示にする RD Web と RD ゲートウェイ エンドポイントです。 ホスト側は、Azure AD アプリケーション プロキシを使用して、完全なデプロイを維持しながら、テナントの環境で仮想マシンの数を縮小できます。 Azure AD アプリケーション プロキシを使用して、多くの利点の条件付きアクセスと多要素認証など、Azure AD が提供することもできます。

詳細については、次を参照してください。[アプリケーション プロキシの概要とコネクタのインストール](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-enable)します。