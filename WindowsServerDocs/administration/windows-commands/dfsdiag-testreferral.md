---
title: dfsdiag TestReferral
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af22520d2c89f9d9f9d91ea6f43a33f3ff9c57f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378363"
---
# <a name="dfsdiag-testreferral"></a>dfsdiag TestReferral

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、DFS\) の参照を \(分散ファイルシステムを確認します。  
  
-   引数を指定せずに DFSpath パラメーターを使用すると、このコマンドは、参照リストにすべての信頼されたドメインが含まれているかどうかを検証します。  
  
-   ドメインを指定すると、コマンドにより、\(dfs diag \/testdcs dc の正常性チェックが実行され、ローカルホストのサイトの関連付けとドメインキャッシュがテストされます。\)  
  
-   ドメインを指定し、SYSvol または \\NETLOGON を \\すると、ドメインを指定したときと同じ正常性チェックを実行するだけでなく、SYSvol または NETLOGON の参照の time To Live \(TTL\) が既定値の900秒と一致するかどうかがチェックされます。  
  
-   名前空間のルートを指定すると、ドメインを指定したときと同じ正常性チェックを実行するだけでなく、DFS 構成チェック \(DFS diag \/TestDFSConfig\) と、DFS diag \/Testdfsconfig\)\(名前空間の整合性チェックが実行されます。  
  
-   DFS フォルダー \(リンク\)を指定すると、名前空間のルートを指定した場合と同じ正常性チェックが実行されるだけでなく、フォルダー \(ターゲットのサイト構成が検証されて、dfs diag \/testsites\)、ローカルホストのサイトの関連付けが検証されます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/DFSpath:<path for getting referrals>|この DFS パスは、次のいずれかになります。<br /><br />-   \(blank\): 信頼されたドメインをテストします。<br />-   \\\\ドメイン: ドメインコントローラーの紹介。<br />-   \\\\ドメイン\\SYSvol: SYSvol 参照。<br />-   \\\\ドメイン\\NETLOGON: NETLOGON の紹介。<br />-   \\\\<Domain or server>\\<Namespace Root>: 名前空間のルート参照。<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS フォルダー \(リンク\) 参照します。|  
|\/完全|ドメインおよびルートの参照にのみ適用されます。 レジストリと active directory ドメインサービス \(AD DS\)間のサイトの関連付け情報の整合性を確認します。|  
  
## <a name="BKMK_Examples"></a>例  
次のように入力します。  
  
```  
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace  
```  
  
次のように入力します。  
  
```  
dfsdiag /TestReferral /DFSpath:  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

