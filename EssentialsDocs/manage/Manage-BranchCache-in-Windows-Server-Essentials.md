---
title: Windows Server Essentials での BranchCache の管理
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f6e05aec-d07c-4e0b-94ab-f20279e9ffd1
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9ef958a34caaffbdcc0b57e8cf63d677e6ab5623
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181028"
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Windows Server Essentials での BranchCache の管理

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

BranchCache は、Windows Server Essentials サーバーがオフィスから離れた場所に配置されている場合、またはローカルサーバーに接続されているクライアントコンピューターが SharePoint Online ライブラリなどのクラウドベースのリソースを使用する場合に、インターネットの使用状況を最適化し、ネットワークアプリケーションのパフォーマンスを向上させ、ワイドエリアネットワーク (WAN) のトラフィックを減らすのに役立ちます

 BranchCache を有効にすると、クライアントコンピューターがリモートの Windows Server Essentials サーバーからコンテンツを要求するときに、コンテンツがローカルオフィスにキャッシュされます。 その後からは、同じオフィス内の別のコンピューターが、WAN を介して対象サーバーのコンテンツを再ダウンロードするのではなく、ローカルに取得できるようになります。 このようにすることによって、ネットワーク接続されたアプリケーションのパフォーマンスを向上させ、WAN を介した帯域幅の消費を削減できます。

 Windows Server Essentials サーバーがローカルかリモートかにかかわらず、BranchCache は、サーバーでホストされているサーバー共有フォルダーと Web コンテンツ (SharePoint Online ライブラリなど) の応答時間を向上させることができます。

 BranchCache では新しいハードウェアの追加やネットワーク トポロジの変更が必要ないため、この機能は、WAN を介してアクセスするサービスとリソースに関して、帯域幅の使用を最適化し、応答時間を短縮するための簡単な方法となります。

## <a name="branchcache-scenarios"></a>BranchCache のシナリオ
 リモート サーバーで BranchCache を使用する基本的なシナリオとして次の 3 つがあります。

-   Windows Server Essentials サーバーは Microsoft Azure でホストされています。

-   Windows Server Essentials サーバーは、サードパーティのサービスプロバイダーのデータセンターでホストされています。

-   お使いの Windows Server Essentials サーバーは、別の場所にある別のオフィスにあります。

## <a name="distributed-cache-mode"></a>分散キャッシュ モード
 Windows Server Essentials では、branchcache は*分散キャッシュモード*で実装されます。これは、branchcache で使用可能な2つのキャッシュモードのうちの1つです。 分散キャッシュ モードでは、ブランチ オフィスのコンテンツ キャッシュがクライアント コンピューター間に分散されます。 ハードウェアを新たに追加したり、トポロジの変更を行ったりする必要がないため、このモードは、リモート サーバーやローカル サーバーを使用して SharePoint Online などのクラウド ベースのサービスにアクセスする小規模なオフィスに適しています。 Windows Server Essentials で BranchCache を有効にすると、分散キャッシュモードが実装されます。

> [!NOTE]
>  複数のサブネットを使用したり、ネットワーク接続されているアプリケーションを使用している従業員が多数いる大規模なブランチ オフィスの場合、*ホスト型キャッシュ モード*で BranchCache を実装すると役立ちます。 ホスト型キャッシュ モードでは、コンテンツ キャッシュは、ブランチ オフィスの 1 つ以上のホスト型キャッシュ サーバーに格納されます。

## <a name="requirements"></a>必要条件
 Windows Server Essentials で BranchCache を使用するには、サーバーとクライアントコンピューターが次の要件を満たしている必要があります。

-   サーバーは、windows server essentials オペレーティングシステム、windows server 2012 R2 Standard、または windows server 2012 R2 Datacenter オペレーティングシステムを Windows Server Essentials エクスペリエンスの役割で実行している必要があります。

     Windows server 2012 R2 Standard または Windows Server 2012 R2 Datacenter Server では、Windows Server Essentials エクスペリエンスの役割を追加すると BranchCache が追加されます。 BranchCache を有効にするには、ドメイン管理者の資格情報を使用して Windows Server Essentials ダッシュボードにサインインする必要があります。

-   クライアントコンピューターは、Windows 7 Enterprise、Windows 7 Ultimate、Windows 8 Enterprise、または Windows 8.1 Enterprise オペレーティングシステムを実行している必要があります。

-   分散キャッシュ モードの場合、すべてのクライアント コンピューターが同じサブネット上になければなりません。

    > [!NOTE]
    >  クライアント コンピューターをドメインに参加することなく Windows Server Essentials サーバーに接続した場合、それらのコンピューターは既定でキャッシング対象から除外されます。 ドメインに参加していないクライアント コンピューターをキャッシング対象に含めるには、クライアント コンピューターで [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) Windows PowerShell コマンドレットを実行してください。 詳細については、「 [Windows PowerShell における BranchCache コマンドレット](https://technet.microsoft.com/library/hh848392.aspx)」を参照してください。


## <a name="turn-branchcache-on"></a>BranchCache を有効にする
 分散キャッシュモードで BranchCache を有効にするには、Windows Server Essentials ダッシュボードのボタンをクリックするだけです。 キャッシュがすぐに開始され、透過的に行われます。

#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>Windows Server Essentials で BranchCache を有効にするには

1.  管理者アカウントを使用して、Windows Server Essentials サーバーにサインインします。

2.  Windows Server Essentials ダッシュボードで、[**設定**] をクリックします。

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

## <a name="additional-references"></a>その他のリファレンス

-   [BranchCache の概要](https://technet.microsoft.com/library/hh831696.aspx)

-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
