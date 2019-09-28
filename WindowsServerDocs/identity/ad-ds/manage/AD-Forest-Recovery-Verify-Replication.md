---
title: AD フォレストの回復-レプリケーションを確認する
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: f65508bf8973721a09c779a52f708d6a258e2cb5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390233"
---
# <a name="resources-to-verify-replication-is-working"></a>レプリケーションが機能していることを確認するためのリソース 

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

すべての Dc を復元または再インストールした後、AD DS と SYSVOL が、Windows Server の任意のバージョンで実行される**repadmin/replsum**を使用して、正常に回復およびレプリケートされていることを確認できます。  
  
> [!TIP]
> また、 [Active Directory Replication Status ツール](https://www.microsoft.com/download/details.aspx?id=30005)(adreplstatus) をダウンロードして実行することもできます。このツールは、dc のレプリケーションの状態を監視し、エラーを報告する無償のツールです。 ADReplStatus には .NET Framework 4 が必要です。これは、まだ存在しない場合にインストールされます。  

イベント ID 4602 (またはファイルレプリケーションサービスイベント ID 13516) の DFS レプリケーションログイベントビューアーを確認します。これは、SYSVOL が初期化されていることを示します。  

最初の回復された DC がイベント ID 4614 ("ドメインコントローラーは初期レプリケーションの実行を待機しています。 レプリケートフォルダーは、パートナー ") が DFS レプリケーションログにレプリケートされるまで初期同期状態のままになります。イベント ID 4602 は表示されず、次の手順でレプリケートされた場合に SYSVOL を回復するには、次の手順を手動で実行する必要があります。DFSR  

1. 最初に復元された DC に DFSR イベント4612が表示されたら、[2218556 の説明に従って、手動で権限のある復元を実行します。DFSR によってレプリケートされた SYSVOL の権限のある同期と権限のない同期を強制的に実行する方法 (FRS の "D4/D2" など) ](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556) 。  
2. 947022で説明されているように、 **SysvolReady フラグ**を手動で1に設定します。これは、 [Active Directory Domain Services を新しいフルまたは読み取り専用の Windows Server 2008 ベースのドメインコントローラーにインストールした後に、NETLOGON 共有が存在しない](https://support.microsoft.com/kb/947022)ことを示します。  

DFS レプリケーション診断レポートを作成することもできます。 詳細については、「 [Windows Server 2008 の DFS レプリケーションと DFS の手順ガイド](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx):[診断レポートの作成](https://technet.microsoft.com/library/cc754227.aspx)」を参照してください。 サーバーで Windows Server 2008 R2 が実行されている場合は、 [Dfsrdiag.exe ReplicationState コマンドラインスイッチ](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)を使用できます。  

また、dcdiag.exe を使用してレプリケーションテストを実行し、レプリケーションエラーを確認することもできます。 詳細については、サポート技術情報の[記事 249256](https://support.microsoft.com/kb/249256)を参照してください。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
