---
title: AD フォレストの回復-レプリケーションを確認する
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: c44f7abd14a65178b84194f43dad829df81fa77b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960834"
---
# <a name="resources-to-verify-replication-is-working"></a>レプリケーションが機能していることを確認するためのリソース 

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

すべての Dc を復元または再インストールした後、AD DS と SYSVOL が、Windows Server の任意のバージョンで実行される**repadmin/replsum**を使用して、正常に回復およびレプリケートされていることを確認できます。  
  
> [!TIP]
> また、 [Active Directory Replication Status ツール](https://www.microsoft.com/download/details.aspx?id=30005)(adreplstatus) をダウンロードして実行することもできます。このツールは、dc のレプリケーションの状態を監視し、エラーを報告する無償のツールです。 ADReplStatus には .NET Framework 4 が必要です。これは、まだ存在しない場合にインストールされます。  

イベント ID 4602 (またはファイルレプリケーションサービスイベント ID 13516) の DFS レプリケーションログイベントビューアーを確認します。これは、SYSVOL が初期化されていることを示します。  

最初の回復された DC がイベント ID 4614 ("ドメインコントローラーは初期レプリケーションの実行を待機しています。 レプリケートフォルダーは、パートナー ") が DFS レプリケーションログにレプリケートされるまで初期同期状態のままになります。その後、イベント ID 4602 は表示されず、DFSR によってレプリケートされた SYSVOL を回復するには、次の手動の手順を実行する必要があります。  

1. 最初に復元された DC に DFSR イベント4612が表示される場合は、「 [2218556: dfsr によってレプリケートされた SYSVOL の権限のある同期と権限のない同期を強制する方法 (FRS の "D4/D2")」 (「」](https://support.microsoft.com/kb/2218556)を参照) を実行します https://support.microsoft.com/kb/2218556) 。  
2. 947022で説明されているように、 **SysvolReady フラグ**を手動で1に設定します。これは、 [Active Directory Domain Services を新しいフルまたは読み取り専用の Windows Server 2008 ベースのドメインコントローラーにインストールした後に、NETLOGON 共有が存在しない](https://support.microsoft.com/kb/947022)ことを示します。  

DFS レプリケーション診断レポートを作成することもできます。 詳細については、「 [Windows Server 2008 の DFS レプリケーションと DFS の手順ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754227(v=ws.11)):[診断レポートの作成](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754227(v=ws.11))」を参照してください。 サーバーで Windows Server 2008 R2 が実行されている場合は、 [dfsrdiag.exe Replicationstate コマンドラインスイッチ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754227(v=ws.11))を使用できます。  

dcdiag.exe を使用してレプリケーションテストを実行し、レプリケーションエラーを確認することもできます。 詳細については、サポート技術情報の[記事 249256](https://support.microsoft.com/kb/249256)を参照してください。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
