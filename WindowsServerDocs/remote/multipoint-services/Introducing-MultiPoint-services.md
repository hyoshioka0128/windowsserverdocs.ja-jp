---
title: MultiPoint Services の概要
description: 複数のユーザーがシステムを共有できるようにするための、MultiPoint Services の概要について説明します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cbef744-4661-4ba9-9e2b-0bbd8854fd5c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: a0497f9dfd39648a94d9fb832f4404491955c06a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395345"
---
# <a name="introducing-multipoint-services"></a>MultiPoint Services の概要
Windows Server 2016 の MultiPoint Services ロールを使用すると、複数のユーザーが独自の独立した使い慣れた Windows エクスペリエンスを持つことで、1台のコンピューターを同時に共有できます。ユーザーがセッションにアクセスするには、いくつかの方法があります。 1つの方法として、任意のデバイスで[リモートデスクトップアプリ](../remote-desktop-services/clients/remote-desktop-clients.md)を使用してサーバーにリモート処理を行う方法があります。 もう1つの方法は、MultiPoint server に接続されているステーションが物理ステーションを使用することです。  
  
-   コンピューターのビデオポートに直接接続します。  
  
-   特殊な usb ゼロクライアント (多機能 USB ハブとも呼ばれます) と同様の USB オーバーイーサネットデバイス。  
  
-   ローカルエリアネットワーク (LAN) 経由  
  
これらの各方法の詳細については、このドキュメントの「 [MultiPoint Services ステーション](MultiPoint-services-Stations.md)」を参照してください。  
  
このドキュメントでは、MultiPoint Services の展開を計画する際に考慮する必要がある次の要素について説明します。  
  
-   MultiPoint Services システムで使用するデスクトップの種類を次に示します。セッション、仮想マシン、または Windows Pc は必要ですか。  
  
-   [MultiPoint Services システムのハードウェアを選択し](Selecting-Hardware-for-Your-MultiPoint-services-System.md)ます。どのようなハードウェアの決定を行う必要がありますか。  
  
-   [ハードウェア要件とパフォーマンスに関する推奨事項](Hardware-Requirements-and-Performance-Recommendations.md):MultiPoint Services にはどのようなハードウェアが必要ですか?  
  
-   [MultiPoint Services サイトの計画](MultiPoint-services-Site-Planning.md):MultiPoint Services を実行しているコンピューターとそのステーションはどこに配置され、どのように構成されますか。  
  
-   [ネットワークに関する考慮事項とユーザーアカウント](Network-Considerations-and-User-Accounts.md):MultiPoint Services システムがデプロイされるネットワーク環境は、ユーザーアカウントの管理方法に影響を与える可能性があります。 ネットワーク環境とは何ですか。 ユーザーアカウントはどのように管理されますか。  
  
-   [MultiPoint Services を使用したファイルの格納](Storing-Files-with-MultiPoint-services.md):ユーザーファイルはどこに格納され、どのようにアクセスされますか。  
  
-   [展開前のチェックリスト](Predeployment-Checklist.md)  