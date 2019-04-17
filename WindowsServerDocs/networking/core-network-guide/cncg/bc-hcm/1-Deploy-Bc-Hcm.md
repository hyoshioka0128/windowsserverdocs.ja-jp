---
title: BranchCache ホスト型キャッシュ モードを展開します。
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 326a1f1edfe6cb763a33ebfc8fd5abdd5b6aab3a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>BranchCache ホスト型キャッシュ モードを展開します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server 2016 コア ネットワーク ガイドを計画およびネットワークが完全に機能し、新しい Active Directory に必要なコア コンポーネントを展開する手順を説明する&reg;新しいフォレスト内のドメイン。

このガイドでは Read\-Only ドメイン コントローラとのクライアント コンピューターが Windows を実行している 1 つまたは複数のブランチ オフィスにホスト型キャッシュ モードで BranchCache を展開するための手順を提供することによって、コア ネットワーク上に構築する方法について説明&reg;10、Windows 8.1、または Windows 8 では、ドメインに参加しているとします。

>[!IMPORTANT]
>展開または Windows Server 2008 R2 を実行している BranchCache ホスト型キャッシュ サーバーが既に展開されていることを計画している場合は、このガイドを使わないでください。 このガイドでは Windows Server を実行しているホスト型キャッシュ サーバーでホスト型キャッシュ モードの展開に関する説明&reg;2016、Windows Server 2012 R2、または Windows Server 2012 です。

このガイドには、次のセクションが含まれています。

- [このガイドを使用するための前提条件](#bkmk_pre)

- [このガイドについて](#bkmk_about)

- [このガイドで説明としていない新機能](#bkmk_not)

- [テクノロジの概要](#bkmk_tech)

- [BranchCache にホスト型キャッシュ モードの展開の概要](2-Bc-Hcm-Deploy-Overview.md)

- [ホスト型キャッシュ モードの BranchCache の展開の計画](3-Bc-Hcm-Plan.md)

- [BranchCache にホスト型キャッシュ モードの展開](4-Bc-Hcm-Deployment.md)

- [その他のリソース](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>このガイドを使用するための前提条件

これは、Windows Server 2016 コア ネットワーク ガイドの必携ガイドです。 このガイドに従ってホスト型キャッシュ モードで BranchCache を展開するには、最初で、次行う必要があります。

- コア ネットワーク ガイドを使用してメイン オフィスにコア ネットワークを展開するか、既にあるテクノロジで提供されるインストールされ、ネットワーク上に正しく機能しているコア ネットワーク ガイド。 これらのテクノロジには、TCP/IP v4、DHCP、Active Directory Domain Services \(AD DS\)、および DNS が含まれます。

    > [!NOTE]
    > Windows Server 2016[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)は、Windows Server 2016 テクニカル ライブラリで利用できます。  

- 実行している Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012、メイン オフィスまたはクラウド データ センターを BranchCache コンテンツ サーバーを展開します。 BranchCache コンテンツ サーバーを展開する方法については、次を参照してください。[その他のリソース](11-Bc-Hcm-additional-resources.md)します。

- ブランチ オフィス、メイン オフィス間のワイド エリア ネットワーク \(WAN\) 接続を確立し、必要に応じて、クラウド リソースを使って仮想プライベート ネットワーク \(VPN\)、DirectAccess、またはその他の接続方法。

- バック グラウンド インテリジェント転送サービス (BITS)、ハイパー テキスト転送プロトコル (HTTP)、およびサーバー メッセージ ブロック (SMB) のサポートに BranchCache を提供する次のオペレーティング システムのいずれかを実行しているブランチ オフィス内のクライアント コンピューターを展開します。
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

>[!NOTE]
>次のオペレーティング システムでは、BranchCache は、HTTP および SMB の機能をサポートしていませんが、BITS の BranchCache 機能をサポートしています。
>     - Windows 10 Pro ビットのみがサポートします。
>     - Windows 8.1 Pro ビットのみがサポートします。
>     - Windows 8 Pro ビットのみがサポートします。

## <a name="bkmk_about"></a>このガイドについて

このガイドは、または Active Directory Domain Services \(AD DS\)、ドメイン ネーム サービス \(DNS\)、動的ホスト構成プロトコル \(DHCP\) など、コア ネットワーク ガイドに含まれるテクノロジが以前に展開するユーザーに対して、コア ネットワークを展開する Windows Server 2016 コア ネットワーク ガイドまたは Windows Server 2012 コア ネットワーク ガイドの指示に従っているネットワークおよびシステム管理者向けに設計されています、TCP/IP v4 とします。

この展開シナリオで使用されているテクノロジのそれぞれの設計と展開のガイドを確認することをお勧めします。 これらのガイドは、この展開シナリオが、サービス、および組織のネットワークに必要な構成を提供するかどうかを判断するのに役立ちます。

## <a name="bkmk_not"></a>このガイドで説明としていない新機能

このガイドでは、BranchCache のモードと機能に関する情報など、BranchCache の概念に関する情報は提供しません。  

このガイドは、WAN 接続または DHCP、RODC、VPN サーバーなど、ブランチ オフィス内の他のテクノロジを展開する方法についての情報を提供していません。

さらに、このガイドでは、ホスト型キャッシュ サーバーを展開するときに使用するハードウェアのガイダンスは紹介はしません。 ホスト型キャッシュ サーバー、ただし、ワークロード、ハードウェアの機能、およびブランチ オフィスの規模に基づいて、決定を行う必要があります、特定のコンピューターで BranchCache ホスト型キャッシュ サーバーをインストールするかどうかと、キャッシュに割り当てるディスク領域の量でその他のサービスとアプリケーションを実行することができます。  
このガイドでは、Windows 7 を実行しているコンピューターを構成する手順については提供されません。 場合は、ブランチ オフィスに Windows 7 を実行しているクライアント コンピューターがある場合は、それらを構成する必要がありますが Windows 10、Windows 8.1、および Windows 8 を実行しているクライアント コンピューターのこのガイドで提供されるものとは異なる手順を使用します。
  
さらに、Windows 7 を実行しているコンピューターがある場合は、クライアント コンピューターを信頼する証明機関によって発行されたサーバー証明書を使用してホスト型キャッシュ サーバーを構成する必要があります。 \ (Windows 10、Windows 8.1、または Windows 8 を実行しているすべてのクライアント コンピューターは場合、は、サーバー証明書で、ホスト型キャッシュ サーバーを構成する必要はありません \)。 
> [!IMPORTANT]
> ホスト型キャッシュ サーバーが Windows Server 2008 R2 を実行している場合は、Windows Server 2008 R2 を使用して[BranchCache 展開ガイド](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx)ホスト型キャッシュ モードで BranchCache を展開するには、このガイドではなく。 すべての BranchCache クライアントを実行しているバージョンの Windows で Windows 7 から Windows 10 には、そのガイドに記載されているグループ ポリシー設定を適用します。 このガイドの手順を使用して、Windows Server 2008 R2 を実行しているコンピューターを構成することはできません。

## <a name="bkmk_tech"></a>テクノロジの概要

この必携ガイドでは、BranchCache はインストールして構成する必要がある唯一のテクノロジです。 Web などのコンテンツ サーバーおよびファイル サーバー上の Windows PowerShell の BranchCache コマンドを実行、ただし必要はありませんを変更するか、他の方法でコンテンツ サーバーを再構成する必要があります。 さらに、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 で AD DS を実行しているドメイン コント ローラーのグループ ポリシーを使用してクライアント コンピューターを構成する必要があります。

### <a name="branchcache"></a>BranchCache

BranchCache は、一部のエディション、Windows Server 2016 および Windows 10 オペレーティング システム、および Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、および Windows 7 の一部のエディションに含まれているワイド エリア ネットワーク (WAN) 帯域幅最適化テクノロジです。

ユーザーがリモート サーバー上のコンテンツをアクセスするときは、WAN 帯域幅を最適化、BranchCache は、クラウドのコンテンツ サーバーをホスト型またはと、他のクライアント コンピューターは WAN を経由ではなくローカルで同じコンテンツにアクセスするブランチ オフィスを許可するブランチ オフィスの場所にコンテンツをキャッシュ メイン オフィスからクライアントから要求されたコンテンツをダウンロードします。

ホスト型キャッシュ モードで BranchCache を展開して、ホスト型キャッシュ モード クライアントとして、ブランチ オフィス内のクライアント コンピューターを構成する必要がありますし、ブランチ オフィス内のホスト型キャッシュ サーバーを展開する必要があります。 このガイドでは、Web からハッシュおよび読み込まれたコンテンツをホスト型キャッシュ サーバーを展開し、ファイル サーバー \ ベースのコンテンツ サーバーする方法について説明します。

### <a name="group-policy"></a>グループ ポリシー

Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 でのグループ ポリシーは、一連の対象とするユーザーと、Active Directory 環境内のコンピューターに必要な構成やポリシー設定の 1 つまたは複数を適用するために使用されるインフラストラクチャです。 

このインフラストラクチャは、グループ ポリシー エンジンとは、ターゲット クライアント コンピューター上のポリシー設定の読み取りを行う複数のクライアント側拡張から \(CSEs\) で構成されます。

グループ ポリシーは、BranchCache ホスト型キャッシュ モードでドメイン メンバー クライアント コンピューターを構成するこのシナリオで使用されます。

このガイドでは、続行するのを参照してください。 [BranchCache ホスト型キャッシュ モードの展開の概要](2-Bc-Hcm-Deploy-Overview.md)します。
