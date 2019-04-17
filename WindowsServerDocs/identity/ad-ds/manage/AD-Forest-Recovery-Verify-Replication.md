---
title: "AD フォレスト回復 - レプリケーションの確認"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adfs
ms.openlocfilehash: d85336a10e808755677a99777af8ecf5c07b05ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="resources-to-verify-replication-is-working"></a>レプリケーションが動作していることを確認するリソース 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
 
 復元されたか、すべての Dc を再インストールした後できることを確認して AD DS と SYSVOL 回復したとレプリケートする正しくを使用して**repadmin/replsum**、任意のバージョンの Windows Server 上で実行します。  
  
> [!TIP]
>  ダウンロードして実行することも、[Active Directory レプリケーションのステータス ツール](https://www.microsoft.com/download/details.aspx?id=30005)(ADReplStatus)、Dc、およびレポートのエラーのレプリケーションの状態を監視する無料のツールです。 ADReplStatus が存在しない場合にインストールされる .NET Framework 4 が必要です。  
  
 SYSVOL が初期化されていることを示すイベント ID 4602 (またはファイル レプリケーション サービスのイベント ID 13516) のイベント ビューアーで、DFS レプリケーション ログを確認します。  
  
 DC ("ドメイン コントローラーが実行を待機して初期レプリケーション イベント ID 4614 をログに記録場合は、最初の回復します。 レプリケート フォルダーは状態のままに、初期同期パートナーとそれがレプリケートされるまで")、DFS レプリケーション ログに、し、イベント ID 4602 は表示されず、DFSR でレプリケートされる場合は、SYSVOL を回復する手動次の手順を実行する必要があります。  
  
1.  復元された最初の dc が表示されたら DFSR イベント 4612」の説明に従って手動 authoritative restore を実行[2218556: ("D4/D2"FRS の) のように、DFSR でレプリケートされた SYSVOL の権限のない同期同期を強制実行する方法](https://support.microsoft.com/kb/2218556)(https://support.microsoft.com/kb/2218556)。  
  
2.  設定**SysvolReady フラグ**1」の説明に従って、手動で[947022、NETLOGON 共有は新しい Windows Server 2008 ベースの完全または読み取り専用ドメイン コントローラーで Active Directory ドメイン サービスをインストールした後に存在しない](https://support.microsoft.com/kb/947022)します。  
  
 DFS レプリケーション診断レポートを作成することもできます。 詳細については、次を参照してください。[DFS レプリケーション診断レポートを作成する](https://technet.microsoft.com/library/cc754227.aspx)と[DFS Step-by-Step Guide Windows Server 2008 用の](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx)します。 サーバーは、Windows Server 2008 R2 を実行しているを使って[dfsrdiag.exe ReplicationState コマンド ライン スイッチ](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)します。  
  
 レプリケーション エラーをチェックする dcdiag.exe を使用してレプリケーションのテストを実行することもできます。 詳細については、サポート技術情報を参照してください。[記事 249256](https://support.microsoft.com/kb/249256)します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
