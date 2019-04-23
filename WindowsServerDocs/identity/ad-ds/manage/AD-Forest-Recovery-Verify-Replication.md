---
title: AD フォレスト回復のレプリケーションを確認します。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: fb05586f281460dc2c7a1afea4c0423493e3fc46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878313"
---
# <a name="resources-to-verify-replication-is-working"></a>レプリケーションの動作を確認するリソース 

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

AD DS と SYSVOL が回復およびレプリケートする正しくを使用して、確認するには復元またはすべての Dc を再インストールした後**repadmin/replsum**、任意のバージョンの Windows Server 上で実行します。  
  
> [!TIP]
> ダウンロードして実行することも、 [Active Directory レプリケーションの状態のツール](https://www.microsoft.com/download/details.aspx?id=30005)(ADReplStatus) ドメイン コント ローラーとレポートのエラーのレプリケーション状態を監視する無料のツール。 ADReplStatus が存在しない場合にインストールされる .NET Framework 4 が必要です。  

イベント ID 4602 (またはファイル レプリケーション サービス イベント ID 13516) は、イベント ビューアで SYSVOL が初期化されていることを示します DFS レプリケーション ログを確認します。  

DC が ("ドメイン コント ローラーを待機している初期レプリケーションを実行イベント ID 4614 を記録する場合、最初の復旧します。 レプリケート フォルダーは残りますが、初期同期状態でそのパートナーとレプリケートされるまで")、DFS レプリケーションのログで、イベント ID 4602 は表示されずしてレプリケートされる場合は、SYSVOL を回復する次の手動手順を実行する必要があります。DFSR:  

1. 最初の復元された dc が表示されたら DFSR イベント 4612」の説明に従って、手動の authoritative restore を実行[2218556。(D2 のような"D4/"for FRS) DFSR でレプリケートされた SYSVOL の権限のない同期同期を強制的に行う方法](https://support.microsoft.com/kb/2218556)(https://support.microsoft.com/kb/2218556)します。  
2. 設定**SysvolReady フラグ**1」の説明に従って、手動で[947022、NETLOGON 共有が存在するは、新しい完全または読み取り専用の Windows Server 2008 ベースのドメイン コント ローラーで Active Directory Domain Services をインストールした後は](https://support.microsoft.com/kb/947022).  

DFS レプリケーション診断レポートを作成することもできます。 詳細については、次を参照してください。 [DFS レプリケーション診断レポートを作成](https://technet.microsoft.com/library/cc754227.aspx)と[DFS ステップ バイ ステップ ガイド Windows Server 2008 用](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx)します。 サーバーで Windows Server 2008 R2 が実行されている場合は使用できます[dfsrdiag.exe ReplicationState コマンド ライン スイッチ](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)します。  

Dcdiag.exe を使用して、レプリケーション エラーをチェックするレプリケーションのテストを実行することもできます。 詳細については、サポート技術情報を参照してください。[記事 249256](https://support.microsoft.com/kb/249256)します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
