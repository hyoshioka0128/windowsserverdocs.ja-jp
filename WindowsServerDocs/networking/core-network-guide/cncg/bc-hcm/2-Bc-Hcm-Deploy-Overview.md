---
title: BranchCache にホスト型キャッシュ モードの展開の概要
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 55686a9c-60dd-47f4-9f1f-fe72c2873a44
ms.author: pashort
author: shortpatti
ms.openlocfilehash: feab3156b89637f64d1af0250df459533b1662c7
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="branchcache-hosted-cache-mode-deployment-overview"></a>BranchCache にホスト型キャッシュ モードの展開の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このガイドを使用して、ブランチ オフィスがドメインに参加しているコンピューターで BranchCache ホスト型キャッシュ サーバーを展開することができます。 このトピックを使用すると、BranchCache ホスト型キャッシュ モードの展開プロセスの概要を取得します。

この概要には、BranchCache のインフラストラクチャ展開の単純な詳細な手順の概要および必要があるにはが含まれています。

## <a name="bkmk_components"></a>ホスト型キャッシュ サーバーの展開のインフラストラクチャ

この展開での Active Directory Domain Services \(AD DS\)、サービス接続ポイントを使用して、ホスト型キャッシュ サーバーが展開されている Windows Server 2016、Windows Server 2012 R2 では、BranchCache は、オプションがあると Web サービスとファイルの共有コンテンツを prehash に、Windows Server 2012 ベースのコンテンツ サーバー、ホスト型キャッシュ サーバー上のコンテンツをプリロードします。

次の図は、BranchCache ホスト型キャッシュ サーバーを展開するために必要なインフラストラクチャを示します。

![BranchCache ホスト型キャッシュ モードの概要](../../../media/BranchCache-Hcm-Overview/Bc-Hcm-Overview.jpg)

> [!IMPORTANT]
> この展開は、クラウド データ センター内のコンテンツ サーバーを示しています、メイン オフィスまたはクラウドの場所に – コンテンツ サーバーを展開するのに関係なく BranchCache ホスト型キャッシュ サーバーを展開するのにこのガイドを使用できます。

### <a name="hcs1-in-the-branch-office"></a>ブランチ オフィス内の HCS1

このコンピューターは、ホスト型キャッシュ サーバーとして構成する必要があります。 ホスト型キャッシュ サーバーでコンテンツをプリロードすることもできるように、コンテンツ サーバー データを prehash を選択する場合は、Web サービスとファイル サーバーからコンテンツが含まれているデータ パッケージをインポートできます。

### <a name="web1-in-the-cloud-data-center"></a>WEB1 で、クラウド データ センター

WEB1 では、BranchCache\ が有効なコンテンツ サーバーです。 コンテンツ サーバー データを prehash、ホスト型キャッシュ サーバーでコンテンツをプリロードすることもできるようにする場合は、WEB1 で、共有コンテンツを prehash し、HCS1 にコピーするデータ パッケージを作成することができます。

### <a name="file1-in-the-cloud-data-center"></a>FILE1 で、クラウド データ センター

FILE1 では、BranchCache\ が有効なコンテンツ サーバーです。 コンテンツ サーバー データを prehash、ホスト型キャッシュ サーバーでコンテンツをプリロードすることもできるようにする場合に、FILE1、上の共有コンテンツを prehash し、HCS1 にコピーするデータ パッケージを作成します。
  
### <a name="dc1-in-the-main-office"></a>メイン オフィスでは DC1

DC1 は、ドメイン コント ローラーと、既定のドメイン ポリシーまたは BranchCache グループ ポリシー設定を自動ホストされるキャッシュの検出サービス接続ポイントによるを有効にすると、展開に合わせて適切なである別のポリシーを構成する必要があります。

ブランチ内のクライアント コンピューターがグループ ポリシーの更新があるし、このポリシー設定が適用されるが自動的に見つけて、ブランチ オフィス内のホスト型キャッシュ サーバーの使用を開始します。

### <a name="client-computers-in-the-branch-office"></a>ブランチ オフィス内のクライアント コンピューター

クライアント コンピューターを新しい BranchCache グループ ポリシー設定を適用して、クライアントを見つけて、ホスト型キャッシュ サーバーを使用できるようにするには、グループ ポリシーを更新する必要があります。

## <a name="bkmk_overview"></a>ホスト型キャッシュ サーバーの展開プロセスの概要

>[!NOTE]
>次の手順を実行する方法の詳細については、セクションで提供されて[BranchCache ホスト型キャッシュ モードの展開](4-Bc-Hcm-Deployment.md)します。

BranchCache ホスト型キャッシュ サーバーを展開するプロセスは、これらの段階で行われます。

>[!NOTE]
>次の手順の一部はオプションですが、これらの手順の事前ハッシュし、ホスト型キャッシュ サーバー上のコンテンツをプリロードする方法を示すなどです。 ホスト型キャッシュ モードで BranchCache を展開するときに必要はありません prehash コンテンツに、Web およびファイル コンテンツ サーバーで、データ パッケージを作成して、ホスト型キャッシュ サーバーのコンテンツをプリロードするために、データ パッケージをインポートします。 手順が記載されて optional としてこのセクションとセクション[BranchCache ホスト型キャッシュ モードの展開](4-Bc-Hcm-Deployment.md)したい場合にスキップするようにします。

1. HCS1 では、ホスト型キャッシュ サーバーとしてコンピューターを構成して、Active Directory にサービス接続ポイントを登録する Windows PowerShell コマンドを使用します。

2. \(Optional\) で HCS1、BranchCache の既定値では、サーバーと、ホスト型キャッシュの展開の目標が一致しない場合は、ホスト型キャッシュに割り当てるディスク領域の量を構成します。 また、ホスト型キャッシュで必要なディスクの場所を構成します。

3. コンテンツ サーバー上の \(Optional\) prehash コンテンツは、ホスト型キャッシュ サーバーでデータ パッケージ、およびコンテンツのプリロードを作成します。

    > [!NOTE]
    > ホスト型キャッシュ サーバーでコンテンツを事前ハッシュと事前読み込みは省略可能、ただし prehash を選択すると、プリロードする必要がありますを実行するすべての手順を次に、展開に適用します。 \ (たとえば、Web サーバーを持っていない場合は必要はありませんの事前ハッシュと事前読み込みが Web サーバーのコンテンツに関連する手順のいずれかを実行する \)。

    1. WEB1 で、Web サーバーのコンテンツを prehash し、データのパッケージを作成します。

    2. FILE1 でファイル サーバーのコンテンツを prehash し、データのパッケージを作成します。

    3. WEB1 と FILE1、HCS1 ホスト型キャッシュ サーバーにデータのパッケージにコピーします。

    4. HCS1、データ キャッシュのプリロードするデータ パッケージをインポートします。

4. DC1 で、BranchCache ポリシーの設定とグループ ポリシーを構成することによって、ホスト型キャッシュ モードのドメインに参加しているブランチ オフィスのクライアント コンピューターを構成します。

5. クライアント コンピューターで、グループ ポリシーを更新します。

このガイドでは、続行するのを参照してください。 [BranchCache ホスト型キャッシュ モードの展開の計画](3-Bc-Hcm-Plan.md)します。