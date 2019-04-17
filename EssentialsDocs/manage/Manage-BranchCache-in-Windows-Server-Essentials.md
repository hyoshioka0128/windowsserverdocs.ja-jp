---
title: "Windows Server Essentials での BranchCache を管理します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e05aec-d07c-4e0b-94ab-f20279e9ffd1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 13d1d439eb9eeb60de9779d783e36405aee3ddfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Windows Server Essentials での BranchCache を管理します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

BranchCache は、インターネットの使用を最適化、ネットワーク上のアプリケーションのパフォーマンスを向上させると、Windows Server Essentials サーバーがあるリモート オフィスからときに、ワイド エリア ネットワーク (WAN) 上のトラフィックを減少させるまたはクライアント コンピューターがローカル サーバーに接続されている場合は、クラウド ベースのリソースを使用して、SharePoint Online ライブラリなどするのに役立ちます。  
  
 BranchCache を有効にすると、クライアント コンピューターがリモートの Windows Server Essentials サーバーのコンテンツからコンテンツを要求するときは、ローカル オフィスにキャッシュされます。 その後、同じオフィス内の他のコンピューターにローカルにダウンロードする代わりに、コンテンツ サーバーからもう一度、WAN 経由でコンテンツを取得できます。 これにより、ネットワーク アプリケーションのパフォーマンスを向上させることができ、WAN 経由で帯域幅の消費を削減します。  
  
 BranchCache は、Windows Server Essentials サーバーは、ローカルまたはリモートには、かどうか、共有サーバー フォルダーと (SharePoint Online ライブラリ) など、サーバーでホストされている Web コンテンツへの応答時間を改善できます。  
  
 BranchCache は、新しいハードウェアやネットワーク トポロジの変更は必要ありません、ためこの機能を使用する帯域幅の使用を最適化し、サービスと、WAN を介してアクセスされるリソースの応答時間を向上するための簡単な方法です。  
  
## <a name="branchcache-scenarios"></a>BranchCache のシナリオ  
 リモート サーバーで BranchCache を使用するための 3 つの基本的なシナリオがあります。  
  
-   Windows Server Essentials サーバーは、Microsoft Azure でホストされます。  
  
-   Windows Server Essentials サーバーは、サード パーティのサービス プロバイダーのデータ センターでホストされています。  
  
-   Windows Server Essentials サーバーでは、他のオフィスに物理的に異なる場所です。  
  
## <a name="distributed-cache-mode"></a>分散キャッシュ モード  
 Windows Server Essentials で BranchCache を実装*分散キャッシュ モード*、BranchCache で使用できる 2 つのキャッシュ モードのいずれかです。 分散キャッシュ モードでは、ブランチ オフィス内のコンテンツ キャッシュはクライアント コンピューター間で配布されます。 必要な追加のハードウェアやトポロジの変更がないために、このモードは、リモート サーバーを使用またはローカル サーバーを使用して SharePoint Online などのクラウド ベースのサービスにアクセスする小規模なオフィスに適して動作します。 Windows Server Essentials で BranchCache を有効にすると、分散キャッシュ モードが実装されます。  
  
> [!NOTE]
>  大規模なブランチ オフィスに複数のサブネットまたはネットワーク対応のアプリケーションを使用する従業員の数が多い、できれば便利で BranchCache を実装する*キャッシュ モード ホストされている*します。 ホスト型キャッシュ モードでのコンテンツ キャッシュは、ブランチ オフィス内の 1 つまたは複数のホスト型キャッシュ サーバーに格納されます。
  
## <a name="requirements"></a>要件  
 Windows Server Essentials で BranchCache を使用するには、サーバーとクライアント コンピューターは、次の要件を満たす必要があります。  
  
-   サーバーは、Windows Server Essentials エクスペリエンス役割を持つ Windows Server Essentials オペレーティング システム、Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter オペレーティング システム、実行する必要があります。  
  
     Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter のサーバーで、Windows Server Essentials Experience 役割を追加すると、BranchCache が追加されます。 BranchCache を有効にするのには、ドメイン管理者の資格情報を持つ Windows Server Essentials ダッシュ ボードにログインする必要があります。  
  
-   クライアント コンピューターでは、Windows 7 Enterprise、Windows 7 Ultimate、Windows 8 Enterprise、または Windows 8.1 Enterprise オペレーティング システムが実行されている必要があります。  
  
-   分散キャッシュ モードでは、すべてのクライアント コンピューターが同じサブネットにする必要があります。  
  
    > [!NOTE]
    >  ドメインへの参加せず、Windows Server Essentials サーバーにクライアント コンピューターを接続している場合は、これらのコンピューターが既定でキャッシュから除外されます。 キャッシュではないドメインに参加しているクライアント コンピューターは、実行、[Enable-bcdistributed](https://technet.microsoft.com/library/hh848398.aspx)、クライアント コンピューターで Windows PowerShell コマンドレット。 詳細については、次を参照してください。[Windows PowerShell の BranchCache コマンドレット](https://technet.microsoft.com/library/hh848392.aspx)します。  
 
  
## <a name="turn-branchcache-on"></a>BranchCache を有効にします。  
 分散キャッシュ モードで BranchCache を有効にするには、単純に、Windows Server Essentials ダッシュ ボード上のボタンをクリックします。 キャッシュがすぐに開始し、透過的に行われます。  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>Windows Server Essentials で BranchCache を有効にするには  
  
1.  管理者アカウントで Windows Server Essentials サーバーにログインします。  
  
2.  Windows Server Essentials ダッシュ ボード] をクリックして**設定**します。  
  
     設定ウィザードが開きます。  
  
3.  をクリックして**BranchCache**します。  
  
4.  **BranchCache 設定**] ページで [**を有効にする**します。  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Windows PowerShell を使用して BranchCache を有効または無効にする  
 BranchCache (有効または無効になっている) の状態を確認して、BranchCache を有効または無効にするには、Windows PowerShell を使用することができます。  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>BranchCache をオンまたはオフ Windows PowerShell を使用するには  
  
1.  サーバーで、管理者として Windows PowerShell を開きます。 **開始**] ページで、右クリック**Windows PowerShell**、] をクリックして**管理者として実行**、] をクリックし、**はい**します。  
  
2.  コマンド プロンプトで次のコマンドレットのいずれかを入力します。  
  
    -   BranchCache (有効または無効になっている) の状態を確認するには、次のように入力します。  
  
        ```powershell  
        Get-WSSBranchCacheStatus  
        ```  
  
    -   BranchCache を有効にするには、次のように入力します。  
  
        ```powershell  
        Enable-WSSBranchCache  
        ```  
  
    -   BranchCache をオフに、次のように入力します。  
  
        ```powershell  
        Disable-WSSBranchCache  
        ```  
  
## <a name="see-also"></a>参照してください。  
    
-   [BranchCache の概要](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)
