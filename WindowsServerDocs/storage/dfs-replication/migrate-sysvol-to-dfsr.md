---
title: SYSVOL のレプリケーションを DFS レプリケーションに移行する
ms.date: 07/02/2012
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 6e022e4fdae631199bacca5f67c7953125ddd141
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950736"
---
# <a name="migrate-sysvol-replication-to-dfs-replication"></a>SYSVOL のレプリケーションを DFS レプリケーションに移行する


更新:2010 年 8 月 25 日

適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008

ドメイン コントローラーでは、SYSVOL という特殊な共有フォルダーを使用して、ログオン スクリプトとグループ ポリシー オブジェクト ファイルを他のドメイン コントローラーにレプリケートします。 Windows 2000 Server および Windows Server 2003 では、ファイル レプリケーション サービス (FRS) を使用して SYSVOL をレプリケートします。一方、Windows Server 2008 では、Windows Server 2008 ドメインの機能レベルを使用するドメインの場合は新しい DFS レプリケーション サービスを、古いドメインの機能レベルを実行するドメインの場合は FRS が使用されます。

SYSVOL フォルダーをレプリケートするために DFS レプリケーションを使用するには、Windows Server 2008 ドメインの機能レベルを使用する新しいドメインを作成するか、このドキュメントで説明されている手順を使用して既存のドメインをアップグレードし、レプリケーションを DFS レプリケーションに移行できます。

このドキュメントでは、Active Directory Domain Services (AD DS)、FRS、および分散ファイル システム レプリケーション (DFS レプリケーション) に関する基本的な知識があることを前提としています。 詳しくは、「[Active Directory Domain Services の概要](https://go.microsoft.com/fwlink/?linkid=147787)」、「[FRS の概要](https://go.microsoft.com/fwlink/?linkid=121763)」、または「[DFS レプリケーションの概要](https://go.microsoft.com/fwlink/?linkid=121762)」をご覧ください。


> [!NOTE]
> このガイドの印刷可能なバージョンをダウンロードするには、「<a href="https://go.microsoft.com/fwlink/?linkid=150375">SYSVOL レプリケーション移行ガイド: FRS から DFS レプリケーション</a>」 (https://go.microsoft.com/fwlink/?LinkId=150375) ) をご覧ください。
<br>


## <a name="in-this-guide"></a>このガイドの内容

[SYSVOL 移行の概念について](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640170(v=ws.10))

  - [SYSVOL 移行の状態](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641052(v=ws.10))

  - [SYSVOL 移行手順の概要](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639809(v=ws.10))


[SYSVOL の移行手順](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639860(v=ws.10))

  - [準備済み状態への移行](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641193(v=ws.10))

  - [リダイレクト済み状態への移行](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641340(v=ws.10))

  - [削除済み状態への移行](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640254(v=ws.10))


[SYSVOL 移行のトラブルシューティング](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640395(v=ws.10))

  - [SYSVOL 移行に関する問題のトラブルシューティング](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639976(v=ws.10))

  - [SYSVOL 移行を以前の安定した状態にロールバック](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640509(v=ws.10))


[SYSVOL 移行参照情報](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd640293(v=ws.10))

  - [サポートされている SYSVOL 移行のシナリオ](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639854(v=ws.10))

  - [SYSVOL 移行の状態を確認する](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639789(v=ws.10))

  - [Dfsrmig](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd641227(v=ws.10))

  - [SYSVOL 移行ツールの操作](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd639712(v=ws.10))


## <a name="additional-references"></a>その他の参照情報

[SYSVOL 移行シリーズ: パート 1—SYSVOL 移行プロセスの概要](https://go.microsoft.com/fwlink/?linkid=121756)

[SYSVOL 移行シリーズ: パート 2—Dfsrmig.exe:SYSVOL 移行ツール](https://go.microsoft.com/fwlink/?linkid=121757)

[SYSVOL 移行シリーズ: パート 3—"準備済み" 状態への移行](https://go.microsoft.com/fwlink/?linkid=121758)

[SYSVOL 移行シリーズ: パート 4—"リダイレクト済み" 状態への移行](https://go.microsoft.com/fwlink/?linkid=121759)

[SYSVOL 移行シリーズ: パート 5—"削除済み" 状態への移行](https://go.microsoft.com/fwlink/?linkid=121760)

[Windows Server 2008 の分散ファイル システムのステップバイステップ ガイド](https://go.microsoft.com/fwlink/?linkid=85231)

[FRS テクニカル リファレンス](https://go.microsoft.com/fwlink/?linkid=121764)
