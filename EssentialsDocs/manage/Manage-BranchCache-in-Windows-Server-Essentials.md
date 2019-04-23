---
title: Windows Server Essentials での BranchCache の管理
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828803"
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Windows Server Essentials での BranchCache の管理

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

インターネットの使用量を最適化、ネットワーク アプリケーションのパフォーマンスが向上し、Windows Server Essentials サーバーがあるリモート オフィスからとき、またはワイド エリア ネットワーク (WAN) 上のトラフィックを削減する BranchCache に役立つクライアント コンピューターSharePoint Online ライブラリなどローカル サーバー使用してクラウド ベース リソースに接続されます。  
  
 Branchcache を有効にすると、クライアント コンピューターがリモートの Windows Server Essentials サーバーのコンテンツからコンテンツを要求するときに、ローカル オフィスにキャッシュされます。 その後からは、同じオフィス内の別のコンピューターが、WAN を介して対象サーバーのコンテンツを再ダウンロードするのではなく、ローカルに取得できるようになります。 このようにすることによって、ネットワーク接続されたアプリケーションのパフォーマンスを向上させ、WAN を介した帯域幅の消費を削減できます。  
  
 Windows Server Essentials サーバーがローカルまたはリモートの場合、BranchCache は、共有サーバー フォルダーと、サーバー (SharePoint Online ライブラリなど) でホストされている Web コンテンツの応答時間を向上できます。  
  
 BranchCache では新しいハードウェアの追加やネットワーク トポロジの変更が必要ないため、この機能は、WAN を介してアクセスするサービスとリソースに関して、帯域幅の使用を最適化し、応答時間を短縮するための簡単な方法となります。  
  
## <a name="branchcache-scenarios"></a>BranchCache のシナリオ  
 リモート サーバーで BranchCache を使用する基本的なシナリオとして次の 3 つがあります。  
  
-   Windows Server Essentials サーバーは、Microsoft Azure でホストされます。  
  
-   Windows Server Essentials サーバーは、サード パーティのサービス プロバイダーのデータ センターでホストされます。  
  
-   Windows Server Essentials サーバーは、別の物理的な場所にある他のオフィスが。  
  
## <a name="distributed-cache-mode"></a>分散キャッシュ モード  
 Windows Server Essentials で BranchCache を実装*分散キャッシュ モード*BranchCache で使用できる 2 つのキャッシュ モードのいずれか。 分散キャッシュ モードでは、ブランチ オフィスのコンテンツ キャッシュがクライアント コンピューター間に分散されます。 ハードウェアを新たに追加したり、トポロジの変更を行ったりする必要がないため、このモードは、リモート サーバーやローカル サーバーを使用して SharePoint Online などのクラウド ベースのサービスにアクセスする小規模なオフィスに適しています。 Windows Server Essentials で BranchCache を有効にすると、分散キャッシュ モードが実装されます。  
  
> [!NOTE]
>  複数のサブネットを使用したり、ネットワーク接続されているアプリケーションを使用している従業員が多数いる大規模なブランチ オフィスの場合、 *ホスト型キャッシュ モード*で BranchCache を実装すると役立ちます。 ホスト型キャッシュ モードでは、コンテンツ キャッシュは、ブランチ オフィスの 1 つ以上のホスト型キャッシュ サーバーに格納されます。
  
## <a name="requirements"></a>必要条件  
 Windows Server Essentials で BranchCache を使用するには、サーバーとクライアント コンピューターは、次の要件を満たす必要があります。  
  
-   サーバーは、Windows Server Essentials エクスペリエンス役割を持つ Windows Server Essentials のオペレーティング システム、Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter オペレーティング システム、実行する必要があります。  
  
     Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter のサーバーで Windows Server Essentials エクスペリエンス役割を追加すると、BranchCache が追加されます。 BranchCache を有効にするのには、ドメイン管理者の資格情報では、Windows Server Essentials のダッシュ ボードにサインインする必要があります。  
  
-   Windows 7 Enterprise、Windows 7 Ultimate、Windows 8 Enterprise、または Windows 8.1 Enterprise オペレーティング システムは、クライアント コンピューターを実行する必要があります。  
  
-   分散キャッシュ モードの場合、すべてのクライアント コンピューターが同じサブネット上になければなりません。  
  
    > [!NOTE]
    >  クライアント コンピューターをドメインに参加することなく Windows Server Essentials サーバーに接続した場合、それらのコンピューターは既定でキャッシング対象から除外されます。 ドメインに参加していないクライアント コンピューターをキャッシング対象に含めるには、クライアント コンピューターで [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) Windows PowerShell コマンドレットを実行してください。 詳細については、「 [Windows PowerShell における BranchCache コマンドレット](https://technet.microsoft.com/library/hh848392.aspx)」を参照してください。  
 
  
## <a name="turn-branchcache-on"></a>BranchCache を有効にする  
 分散キャッシュ モード BranchCache を有効にするには、単に、Windows Server Essentials ダッシュ ボード上のボタンをクリックします。 キャッシュがすぐに開始され、透過的に行われます。  
  
#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>Windows Server Essentials で BranchCache を有効にするには  
  
1.  管理者アカウントで Windows Server Essentials サーバーにサインインします。  
  
2.  Windows Server Essentials ダッシュ ボードで、次のようにクリックします。**設定**します。  
  
     セットアップ ウィザードが開きます。  
  
3.  **[BranchCache]** をクリックします。  
  
4.  **[BranchCache 設定]** ページで、 **[有効にする]** をクリックします。  
  
## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Windows PowerShell を使用して BranchCache の有効と無効を切り替える  
 Windows PowerShell を使用して、BranchCache の状態 (有効または無効) を確認し、BranchCache の有効または無効を切り替えることができます。  
  
#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>BranchCache の有効または無効を Windows PowerShell を使用して切り替えるには  
  
1.  サーバーで、管理者として Windows PowerShell を開きます。 **[スタート]** ページで、**[Windows PowerShell**] を右クリックし、**[管理者として実行]**、**[はい]** の順にクリックします。  
  
2.  コマンド プロンプトで、次のいずれかのコマンドレットを実行します。  
  
    -   BranchCache の状態 (有効または無効) を確認する場合には、次のように入力します。  
  
        ```powershell  
        Get-WSSBranchCacheStatus  
        ```  
  
    -   BranchCache を有効にする場合、次のように入力します。  
  
        ```powershell  
        Enable-WSSBranchCache  
        ```  
  
    -   BranchCache を無効にする場合、次のように入力します。  
  
        ```powershell  
        Disable-WSSBranchCache  
        ```  
  
## <a name="see-also"></a>関連項目  
    
-   [BranchCache の概要](https://technet.microsoft.com/library/hh831696.aspx)  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)
