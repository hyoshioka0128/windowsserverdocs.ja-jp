---
title: BranchCache ホスト型キャッシュ モードの展開計画
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: bc44a7db-f7a5-4e95-9d95-ab8d334e885f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 09e6d6db0347e36c2cea01a0bc200edcaf4eb474
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319055"
---
# <a name="branchcache-hosted-cache-mode-deployment-planning"></a>BranchCache ホスト型キャッシュ モードの展開計画

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックを使用して、ホスト型キャッシュモードで BranchCache の展開を計画することができます。

>[!IMPORTANT]
>ホスト型キャッシュサーバーでは、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 が実行されている必要があります。

ホスト型キャッシュサーバーを配置する前に、次の項目を計画する必要があります。

- [基本的なサーバー構成の計画](#bkmk_basic)

- [ドメインアクセスを計画する](#bkmk_domain)

- [ホスト型キャッシュの場所とサイズを計画する](#bkmk_cachelocation)

- [コンテンツサーバーパッケージのコピー先の共有を計画する](#bkmk_package)

- [コンテンツサーバーでの事前ハッシュとデータパッケージの作成を計画する](#bkmk_prehash)

## <a name="plan-basic-server-configuration"></a><a name="bkmk_basic"></a>基本的なサーバー構成の計画
  
ブランチオフィス内の既存のサーバーをホスト型キャッシュサーバーとして使用する予定がある場合は、この計画手順を実行する必要はありません。これは、コンピューターに既にという名前が付けられ、IP アドレス構成があるためです。

ホスト型キャッシュサーバーに Windows Server 2016 をインストールした後で、コンピューターの名前を変更し、ローカルコンピューターの静的 IP アドレスを割り当てて構成する必要があります。

>[!NOTE]
>このガイドでは、ホスト型キャッシュサーバーには HCS1 という名前が付けられていますが、展開に適したサーバー名を使用する必要があります。

## <a name="plan-domain-access"></a><a name="bkmk_domain"></a>ドメインアクセスを計画する

ブランチオフィス内の既存のサーバーをホスト型キャッシュサーバーとして使用する予定の場合は、コンピューターが現在ドメインに参加していない限り、この計画手順を実行する必要はありません。
  
ドメインにログオンするには、コンピューターがドメイン メンバー コンピューターをする必要があり、ログオン試行の前に AD DS でユーザー アカウントを作成する必要があります。 さらに、適切なグループメンバーシップを持つアカウントを使用して、コンピューターをドメインに参加させる必要があります。

## <a name="plan-the-location-and-size-of-the-hosted-cache"></a><a name="bkmk_cachelocation"></a>ホスト型キャッシュの場所とサイズを計画する

HCS1 で、ホスト型キャッシュサーバー上のホスト型キャッシュを配置する場所を決定します。 たとえば、キャッシュを格納するハードディスク、ボリューム、およびフォルダーの場所を決定します。

さらに、ホスト型キャッシュに割り当てるディスク領域の割合を決定します。

## <a name="plan-the-share-to-which-the-content-server-packages-are-to-be-copied"></a><a name="bkmk_package"></a>コンテンツサーバーパッケージのコピー先の共有を計画する

コンテンツサーバーにデータパッケージを作成した後は、ホスト型キャッシュサーバー上の共有にネットワーク経由でデータパッケージをコピーする必要があります。

共有フォルダーのフォルダーの場所と共有のアクセス許可を計画します。 また、コンテンツサーバーが大量のデータをホストしていて、作成するパッケージが大きなファイルである場合は、他のユーザーが使用する必要がある時間帯に WAN 帯域幅が消費されないように、ピーク時間外にコピー操作を実行することを計画します。通常のビジネス操作の帯域幅。

## <a name="plan-prehashing-and-data-package-creation-on-content-servers"></a><a name="bkmk_prehash"></a>コンテンツサーバーでの事前ハッシュとデータパッケージの作成を計画する

コンテンツサーバーにコンテンツを事前にハッシュする前に、データパッケージに追加するコンテンツが含まれているフォルダーとファイルを特定する必要があります。 

また、データパッケージをホスト型キャッシュサーバーにコピーする前に、データパッケージを格納できるローカルフォルダーの場所を計画する必要があります。

このガイドを続行するには、「 [BranchCache ホスト型キャッシュモードの展開](4-Bc-Hcm-Deployment.md)」を参照してください。
