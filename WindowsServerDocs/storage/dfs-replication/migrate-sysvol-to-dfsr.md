---
title: SYSVOL のレプリケーションを DFS レプリケーションに移行する
ms.date: 07/02/2012
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 56877bc5ddb3ea5f24f4057051775094654d8bbf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386036"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>SYSVOL のレプリケーションを DFS レプリケーションに移行する


更新:2010年8月25日

適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008

ドメインコントローラーは、SYSVOL という特殊な共有フォルダーを使用して、ログオンスクリプトとグループポリシーオブジェクトファイルを他のドメインコントローラーにレプリケートします。 Windows 2000 Server および Windows Server 2003 では、ファイルレプリケーションサービス (FRS) を使用して SYSVOL をレプリケートします。一方、windows server 2008 では、Windows Server 2008 ドメインの機能レベルを使用するドメインの場合は、新しい DFS レプリケーションサービスを使用します。古いドメインの機能レベルを実行します。

SYSVOL フォルダーをレプリケートするために DFS レプリケーションを使用するには、Windows Server 2008 ドメインの機能レベルを使用する新しいドメインを作成するか、このドキュメントで説明されている手順を使用して既存のドメインをアップグレードし、レプリケーションをに移行します。DFS レプリケーション。

このドキュメントでは、Active Directory Domain Services (AD DS)、FRS、分散ファイルシステムレプリケーション (DFS レプリケーション) に関する基本的な知識があることを前提としています。 詳細については、「 [Active Directory Domain Services の概要](http://go.microsoft.com/fwlink/?linkid=147787)」、「 [FRS の概要](http://go.microsoft.com/fwlink/?linkid=121763)」、または「概要」を参照してください[DFS レプリケーション](http://go.microsoft.com/fwlink/?linkid=121762)


> [!NOTE]
> このガイドの印刷可能なバージョンをダウンロードするに<a href="http://go.microsoft.com/fwlink/?linkid=150375">は、「SYSVOL レプリケーション移行ガイド:FRS を DFS レプリケーション</a> (http://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>このガイドについて

[SYSVOL 移行の概念情報](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL 移行の状態](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [SYSVOL 移行手順の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL の移行手順](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [準備済み状態への移行](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [リダイレクトされた状態への移行](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [削除された状態への移行](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[SYSVOL 移行のトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [SYSVOL の移行に関する問題のトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [SYSVOL 移行を以前の安定した状態にロールバックしています](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[SYSVOL 移行の参照情報](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [サポートされている SYSVOL 移行シナリオ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [SYSVOL 移行の状態を確認しています](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [Dfsrmig](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [SYSVOL 移行ツールの操作](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>その他の参照情報

[SYSVOL 移行シリーズ:パート 1-SYSVOL 移行プロセスの概要](http://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL 移行シリーズ:パート 2-Dfsrmig:SYSVOL 移行ツール](http://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL 移行シリーズ:パート 3: ' 準備済み ' 状態への移行](http://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL 移行シリーズ:パート 4: "リダイレクト" 状態への移行](http://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL 移行シリーズ:パート 5: "廃止" 状態への移行](http://go.microsoft.com/fwlink/?linkid=121760)

[Windows Server 2008 の分散ファイルシステムのステップバイステップガイド](http://go.microsoft.com/fwlink/?linkid=85231)

[FRS テクニカルリファレンス](http://go.microsoft.com/fwlink/?linkid=121764)

