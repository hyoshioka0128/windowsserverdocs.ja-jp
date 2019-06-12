---
title: BranchCache ホスト型キャッシュ モードを展開する
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 54991b343623b934118bb62af1bd91871a726996
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446483"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>BranchCache ホスト型キャッシュ モードを展開する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server 2016 コア ネットワーク ガイドの計画とネットワークが完全に機能し、新しい Active Directory に必要なコア コンポーネントを展開するための手順を提供する&reg;新しいフォレストのドメイン。

このガイドを読み取り、1 つまたは複数のブランチ オフィスでホスト型キャッシュ モードで BranchCache を展開するための手順を提供することで、コア ネットワーク上に構築する方法を説明する\-クライアント コンピューターに Windows が実行されているドメイン コント ローラーのみ&reg;10、Windows 8.1、または Windows 8 では、ドメインに参加しているとします。

>[!IMPORTANT]
>展開または Windows Server 2008 R2 を実行している BranchCache ホスト型キャッシュ サーバーが既に展開を計画している場合は、このガイドを使用しないでください。 このガイドでは Windows Server を実行しているホスト型キャッシュ サーバーとホスト型キャッシュ モードの展開の説明&reg;2016、Windows Server 2012 R2、または Windows Server 2012。

このガイドは次のセクションで構成されます。

- [このガイドを使用するための前提条件](#bkmk_pre)

- [このガイドについて](#bkmk_about)

- [このガイドで説明されていないもの](#bkmk_not)

- [テクノロジの概要](#bkmk_tech)

- [BranchCache ホスト型キャッシュ モードの展開の概要](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache には、キャッシュ モードがホストされている展開の計画](3-Bc-Hcm-Plan.md)

- [BranchCache にホスト型キャッシュ モードの展開](4-Bc-Hcm-Deployment.md)

- [その他のリソース](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>このガイドを使用するための前提条件

これは、Windows Server 2016 コア ネットワーク ガイドの必携ガイドです。 このガイドに従ってホスト型キャッシュ モードで BranchCache をデプロイするには、先に次のことを行う必要があります。

- コア ネットワーク ガイドを使用してメイン オフィスにコア ネットワークをデプロイするか、コア ネットワーク ガイドで説明されているテクノロジが既にネットワーク上に正しくインストールされて機能している必要があります。 これらのテクノロジは、TCP\/IP v4、DHCP、Active Directory Domain Services \(AD DS\)、および DNS。

    > [!NOTE]
    > Windows Server 2016[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)は、Windows Server 2016 テクニカル ライブラリで使用できます。  

- メイン オフィスまたはクラウド データ センターの Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行する BranchCache コンテンツ サーバーをデプロイします。 BranchCache コンテンツ サーバーをデプロイする方法については、次を参照してください。[資料](11-Bc-Hcm-additional-resources.md)します。

- ワイド エリア ネットワークを確立\(WAN\) 、ブランチ オフィス、メイン オフィス間の接続と、該当する場合は、仮想プライベート ネットワークを使用して、クラウド リソース\(VPN\)DirectAccess、またはその他接続方法。

- BranchCache をバック グラウンド インテリジェント転送サービス (BITS)、ハイパー テキスト転送プロトコル (HTTP)、およびサーバー メッセージ ブロック (SMB) のサポートを提供する次のオペレーティング システムのいずれかを実行しているブランチ オフィス内のクライアント コンピューターを展開します.
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

> [!NOTE]
> 次のオペレーティング システムでは、BranchCache は、HTTP と SMB の機能をサポートしていませんが BITS の BranchCache 機能をサポートします。
>     - Windows 10 Pro BITS サポートのみ
>     - Windows 8.1 Pro BITS サポートのみ
>     - Windows 8 Pro BITS サポートのみ

## <a name="bkmk_about"></a>このガイドについて

このガイドは、コア ネットワークをデプロイする、Windows Server 2016 コア ネットワーク ガイド Windows Server 2012 コア ネットワーク ガイドの手順に従っているネットワークとシステムの管理者または以前にデプロイした方のために設計されていますが、Active Directory Domain Services を含む、コア ネットワーク ガイドで使用されているテクノロジ\(AD DS\)、ドメイン ネーム サービス\(DNS\)、動的ホスト構成プロトコル\(DHCP\)、および TCP\/IP v4 です。

このデプロイ シナリオで使用される各テクノロジについては、それぞれの設計ガイドやデプロイ ガイドを参照することをお勧めします。 これらのガイドは、このデプロイ シナリオが組織のネットワークに必要なサービスおよび構成を提供するかどうかを判断するのに役立ちます。

## <a name="bkmk_not"></a>このガイドで説明としていないもの

このガイドでは、BranchCache のモードと機能に関する情報など、BranchCache の概念に関する情報は提供しません。  

このガイドでは、WAN 接続またはブランチ オフィス内の他のテクノロジ (DHCP、RODC、VPN サーバーなど) をデプロイする方法についての情報は提供しません。

さらに、このガイドではホスト型キャッシュ サーバーをデプロイするときに使用するハードウェアについてのガイダンスは提供しません。 ホスト型キャッシュ サーバーで他のサービスやアプリケーションを実行することもできますが、ワークロード、ハードウェアの機能、およびブランチ オフィスの規模に基づいて、特定のコンピューターに BranchCache ホスト型キャッシュ サーバーをインストールするかどうか、およびキャッシュに割り当てるディスク領域の量を、判断する必要があります。  
このガイドでは、Windows 7 を実行しているコンピューターを構成する手順については提供されません。 ブランチ オフィスで Windows 7 を実行しているクライアント コンピューターをした場合、それらを構成する必要がありますが、Windows 10、Windows 8.1、および Windows 8 を実行しているクライアント コンピューターのこのガイドで提供されるものとは異なる手順を使用します。
  
さらに、Windows 7 を実行しているコンピューターがある場合は、クライアント コンピューターを信頼する証明機関によって発行されたサーバー証明書に、ホスト型キャッシュ サーバーを構成する必要があります。 \(Windows 10、Windows 8.1、または Windows 8 を実行しているすべてのクライアント コンピューターは場合、は、サーバー証明書とホスト型キャッシュ サーバーを構成する必要はありません。\) 
> [!IMPORTANT]
> ホスト型キャッシュ サーバーが Windows Server 2008 R2 を実行している場合は、Windows Server 2008 R2 を使用して[BranchCache 展開ガイド](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx)ホスト型キャッシュ モードで BranchCache をデプロイするには、このガイドではなく。 Windows 7 から Windows 10 のバージョンの Windows を実行するすべての BranchCache クライアントにそのガイドに記載されているグループ ポリシー設定を適用します。 このガイドの手順を使用して、Windows Server 2008 R2 を実行しているコンピューターを構成することはできません。

## <a name="bkmk_tech"></a>テクノロジの概要

この必携ガイドでインストールして構成する必要のあるテクノロジは、BranchCache だけです。 Web サーバーやファイル サーバーなどのコンテンツ サーバーで Windows PowerShell の BranchCache コマンドを実行する必要がありますが、それ以外の変更や構成をコンテンツ サーバーで行う必要はありません。 さらに、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 で AD DS を実行しているドメイン コント ローラーにグループ ポリシーを使用して、クライアント コンピューターを構成する必要があります。

### <a name="branchcache"></a>BranchCache

BranchCache は Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8 の一部のエディションの Windows Server 2016 および Windows 10 オペレーティング システムでは、一部のエディションに組み込まれているワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジ、Windows Server 2008 R2、および Windows 7。

WAN の帯域幅を最適化するには、ユーザーがリモート サーバー上のコンテンツにアクセスするには、BranchCache をメイン オフィスからコンテンツをクライアントが要求をダウンロードまたはクラウド コンテンツ サーバーをホストし、その他のクライアント コンピュータを許可するブランチ オフィスの場所にコンテンツをキャッシュブランチ オフィス、WAN 経由ではなく、ローカルで同じコンテンツにアクセスします。

ホスト型キャッシュ モードで BranchCache をデプロイするときは、ブランチ オフィスのクライアント コンピューターをホスト型キャッシュ モード クライアントとして構成した後、ホスト型キャッシュ サーバーをブランチ オフィスにデプロイする必要があります。 このガイドは、Web サービスとファイル サーバーからのハッシュおよび読み込まれたコンテンツを持つホスト型キャッシュ サーバーをデプロイする方法を示します\-ベースのサーバーのコンテンツ。

### <a name="group-policy"></a>グループ ポリシー

Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 でのグループ ポリシーは、インフラストラクチャを提供および一連の対象とするユーザーと、Active Directory 環境内のコンピューターに必要な構成やポリシー設定の 1 つまたは複数を適用するために使用します。 

このインフラストラクチャは、グループ ポリシー エンジンと複数のクライアントで構成されます\-側拡張機能\(Cse\)ターゲット クライアント コンピューター上のポリシー設定の読み取りを担当しています。

このシナリオでのグループ ポリシーは、BranchCache ホスト型キャッシュ モードでドメイン メンバー クライアント コンピューターを構成するために使用されます。

このガイドを続行する、次を参照してください。 [BranchCache ホスト キャッシュ モードの展開の概要](2-Bc-Hcm-Deploy-Overview.md)します。
