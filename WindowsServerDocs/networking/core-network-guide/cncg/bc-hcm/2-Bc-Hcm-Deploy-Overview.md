---
title: BranchCache ホスト型キャッシュ モードの展開の概要
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 930a9b4872a7a79351055841a5d716dd99df0fa9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829513"
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>BranchCache ホスト型キャッシュ モードの展開の概要

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このガイドを使用して、コンピューターがドメインに参加しているブランチ オフィスに BranchCache ホスト型キャッシュ サーバーをデプロイすることができます。 このトピックを使用すると、BranchCache ホスト型キャッシュ モードの展開プロセスの概要を取得します。

この概要には、展開の簡単なステップ バイ ステップの概要と、必要な BranchCache インフラストラクチャが含まれています。

## <a name="bkmk_components"></a>ホスト型キャッシュ サーバーの展開インフラストラクチャ

サービス接続ポイントを Active Directory Domain Services を使用してこの展開で、ホスト型キャッシュ サーバーが展開されている\(AD DS\)、Windows Server 2016、Windows Server 2012 R2、および Windows の BranchCache は、オプションを使用してWeb サービスとファイルの共有のコンテンツをプリハッシュして、server 2012 ベースのコンテンツ サーバー、し、ホスト型キャッシュ サーバー上のコンテンツをプリロードします。

次の図は、BranchCache ホスト型キャッシュ サーバーを展開するために必要なインフラストラクチャを示します。

![BranchCache ホスト型キャッシュ モードの概要](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> この展開では、クラウドのデータ センター内のコンテンツ サーバーを示し、メイン オフィスまたはクラウドの場所に – コンテンツ サーバーを展開するのに関係なく BranchCache ホスト型キャッシュ サーバーを展開するのにこのガイドを使用できます。

### <a name="hcs1-in-the-branch-office"></a>ブランチ オフィスで HCS1

このコンピューターは、ホスト型キャッシュ サーバーとして構成する必要があります。 ホスト型キャッシュ サーバーでコンテンツをプリロードするように、コンテンツ サーバーのデータを prehash を選択する場合は、Web サービスとファイル サーバーからコンテンツを含むデータ パッケージをインポートできます。

### <a name="web1-in-the-cloud-data-center"></a>WEB1 で、クラウド データ センター

WEB1 は、BranchCache\-コンテンツ サーバーを有効にします。 ホスト型キャッシュ サーバーでコンテンツをプリロードするように、コンテンツ サーバーのデータを prehash を選択した場合に、WEB1 で、共有のコンテンツを prehash し、HCS1 にコピーするデータのパッケージを作成します。

### <a name="file1-in-the-cloud-data-center"></a>クラウドのデータ センターで FILE1

FILE1、BranchCache は、\-コンテンツ サーバーを有効にします。 ホスト型キャッシュ サーバーでコンテンツをプリロードするように、コンテンツ サーバーのデータを prehash を選択した場合に、FILE1 上の共有のコンテンツを prehash し、HCS1 にコピーするデータのパッケージを作成します。
  
### <a name="dc1-in-the-main-office"></a>メイン オフィスで DC1

DC1 は、ドメイン コント ローラーと、既定のドメイン ポリシー、またはサービス接続ポイントでの自動ホストされるキャッシュ検出を有効にする BranchCache グループ ポリシー設定で、展開に適した別のポリシーを構成する必要があります。

ブランチ内のクライアント コンピューターがあるグループ ポリシーを更新し、このポリシー設定が適用されると、ときに、自動的に見つけて、ブランチ オフィスでホスト型キャッシュ サーバーの使用を開始します。

### <a name="client-computers-in-the-branch-office"></a>ブランチ オフィス内のクライアント コンピューター

新しい BranchCache グループ ポリシー設定を適用して、クライアントが検索し、ホスト型キャッシュ サーバーを使用できるように、クライアント コンピューターでは、グループ ポリシーを更新する必要があります。

## <a name="bkmk_overview"></a>ホスト型キャッシュ サーバーの展開プロセスの概要

>[!NOTE]
>これらの手順を実行する方法の詳細については、セクションで説明[BranchCache ホスト キャッシュ モードの配置](4-Bc-Hcm-Deployment.md)します。

BranchCache ホスト型キャッシュ サーバーをデプロイするプロセスは、これらのステージで発生します。

>[!NOTE]
>次の手順の一部は省略可能なこれらの手順を prehash し、ホスト型キャッシュ サーバー上のコンテンツをプリロードする方法を示すなど。 ホスト型キャッシュ モードで BranchCache を展開するときに必要はありません prehash コンテンツに、Web サービスとファイル コンテンツ サーバーで、データ パッケージを作成して、コンテンツを含む、ホスト型キャッシュ サーバーをプリロードするために、データ パッケージをインポートします。 セクションのこのセクションでは、手順は省略可能としてまとめます[BranchCache ホスト キャッシュ モードの配置](4-Bc-Hcm-Deployment.md)したい場合は、スキップできるようにします。

1. HCS1 には、ホスト型キャッシュ サーバーとしてコンピューターを構成して、Active Directory でサービス接続ポイントを登録する Windows PowerShell コマンドを使用します。

2. \(省略可能な\)で HCS1、BranchCache の既定値には、サーバーとホストのキャッシュで、展開の目標が一致しない場合はホスト型キャッシュに割り当てるディスク領域の量を構成します。 また、ホスト型キャッシュで望ましいとディスクの場所を構成します。

3. \(省略可能な\)コンテンツ サーバー上のコンテンツを Prehash、データのパッケージを作成およびホスト型キャッシュ サーバー上のコンテンツをプリロードします。

    > [!NOTE]
    > ホスト型キャッシュ サーバーでコンテンツを事前ハッシュおよびプリロードは省略可能、ただしファイルサーバーを選択して、プリロードする必要がありますすべてを実行する手順を次の場合、デプロイに適用できます。 \(たとえば、Web サーバーがない、いずれかの事前ハッシュおよび Web サーバーのコンテンツを事前読み込みに関連する手順を実行する必要はありません。\)

    1. WEB1 で、Web サーバーのコンテンツを prehash し、データ パッケージを作成します。

    2. FILE1 でファイル サーバーのコンテンツを prehash し、データ パッケージを作成します。

    3. WEB1 FILE1 から HCS1 ホスト型キャッシュ サーバーにデータ パッケージをコピーします。

    4. HCS1、データ キャッシュを事前にデータ パッケージをインポートします。

4. DC1 で、BranchCache ポリシーの設定とグループ ポリシーを構成することで、ホスト型キャッシュ モードのドメインに参加してブランチ オフィスのクライアント コンピューターを構成します。

5. クライアント コンピューターでは、グループ ポリシーを更新します。

このガイドを続行する、次を参照してください。 [BranchCache ホスト キャッシュ モードの展開の計画](3-Bc-Hcm-Plan.md)します。