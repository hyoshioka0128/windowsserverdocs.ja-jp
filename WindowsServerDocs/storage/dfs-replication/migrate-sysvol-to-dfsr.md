---
Title: SYSVOL のレプリケーションを DFS レプリケーションに移行する
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 30b3c5925971a2709ba422a017a73f47e72813a7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284432"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>SYSVOL のレプリケーションを DFS レプリケーションに移行する


更新:2010 年 8 月 25 日

適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008

ドメイン コント ローラーでは、SYSVOL をという名前の特別な共有フォルダーを使用して、ログオン スクリプトとグループ ポリシー オブジェクトのファイルを他のドメイン コント ローラーにレプリケートします。 Windows 2000 Server および Windows Server 2003 が、Windows Server 2008 では Windows Server 2008 のドメイン機能レベルを使用するドメインで新しい DFS レプリケーション サービス、SYSVOL をレプリケートするように、ファイル レプリケーション サービス (FRS) およびドメインの FRS を使用します。以前のドメイン機能レベルを実行します。

DFS レプリケーションを使用して、SYSVOL フォルダーをレプリケートする、Windows Server 2008 のドメイン機能レベルを使用する新しいドメインを作成するかまたは既存のドメインをアップグレードしへのレプリケーションを移行するには、このドキュメントで説明されている手順を使用することができます。DFS レプリケーション。

このドキュメントでは、Active Directory Domain Services (AD DS)、FRS、および分散ファイル システム レプリケーション (DFS レプリケーション) の基本的な知識があることを前提としています。 詳細については、次を参照してください[Active Directory Domain Services の概要](http://go.microsoft.com/fwlink/?linkid=147787)、 [FRS の概要](http://go.microsoft.com/fwlink/?linkid=121763)、または[DFS レプリケーションの概要。](http://go.microsoft.com/fwlink/?linkid=121762)


> [!NOTE]
> このガイドの印刷可能なバージョンをダウンロードするには<a href="http://go.microsoft.com/fwlink/?linkid=150375">SYSVOL レプリケーション移行ガイド。FRS DFS レプリケーションから</a>(http://go.microsoft.com/fwlink/?LinkId=150375)
<br>


## <a name="in-this-guide"></a>このガイドについて

[SYSVOL の移行の概念について](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640170(v=ws.10))

  - [SYSVOL の移行の状態](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641052(v=ws.10))  
      
  - [SYSVOL の移行手順の概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639809(v=ws.10))  
      

[SYSVOL の移行手順](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639860(v=ws.10))

  - [準備された状態に移行します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641193(v=ws.10))  
      
  - [リダイレクトされた状態に移行します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641340(v=ws.10))  
      
  - [削除された状態に移行します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640254(v=ws.10))  
      

[SYSVOL の移行のトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640395(v=ws.10))

  - [SYSVOL の移行に関する問題のトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639976(v=ws.10))  
      
  - [以前の安定した状態に SYSVOL の移行をロールバックしています](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640509(v=ws.10))  
      

[SYSVOL の移行の参照情報](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd640293(v=ws.10))

  - [サポートされている SYSVOL の移行シナリオ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639854(v=ws.10))  
      
  - [SYSVOL の移行の状態を確認しています](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639789(v=ws.10))  
      
  - [dfsrmig](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd641227(v=ws.10))  
      
  - [SYSVOL の移行ツールの操作](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd639712(v=ws.10))  
      

## <a name="additional-references"></a>その他の参照情報

[SYSVOL の移行シリーズ:第 1 部: SYSVOL の移行プロセスの概要](http://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL の移行シリーズ:一部の 2—Dfsrmig.exe:SYSVOL の移行ツール](http://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL の移行シリーズ:パート 3-'を ' 準備状態に移行します。](http://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL の移行シリーズ:パート 4-'リダイレクトされた状態に移行します。](http://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL の移行シリーズ:パート 5-'削除' の状態に移行します。](http://go.microsoft.com/fwlink/?linkid=121760)

[Windows Server 2008 での分散ファイル システムのステップ バイ ステップ ガイド](http://go.microsoft.com/fwlink/?linkid=85231)

[FRS テクニカル リファレンス](http://go.microsoft.com/fwlink/?linkid=121764)

