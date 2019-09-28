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

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次のテストを実行して、分散ファイルシステム @no__t 0DFS @ no__t の紹介を確認します。  
  
-   引数を指定せずに DFSpath パラメーターを使用すると、このコマンドは、参照リストにすべての信頼されたドメインが含まれているかどうかを検証します。  
  
-   ドメインを指定すると、コマンドによってドメインコントローラーの正常性チェックが実行されます。 \(dfsdiag \/testdcs @ no__t から、ローカルホストのサイトの関連付けとドメインキャッシュをテストします。  
  
-   ドメインを指定し、\\SYSvol または \\NETLOGON を指定した場合、ドメインを指定したときと同じ正常性チェックを実行するだけでなく、コマンドは、time To Live \(TTL @ no__t of SYSvol または NETLOGON 参照が既定値 () と一致することを確認します。900秒。  
  
-   名前空間のルートを指定すると、ドメインを指定したときと同じ正常性チェックを実行するだけでなく、DFS の構成チェック \(dfsdiag \/TestDFSConfig @ no__t と名前空間の整合性チェック \(dfsdiag \/TestDFSIntegrity @ no__t-5。  
  
-   DFS フォルダー \(link @ no__t-1 を指定した場合、名前空間のルートを指定したときと同じ正常性チェックを実行するだけでなく、フォルダーターゲットのサイト構成が検証され \(dfsdiag \/testsites @ no__t-4 と検証されます。ローカルホストのサイトの関連付け。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/DFSpath: <path for getting referrals>|この DFS パスは、次のいずれかになります。<br /><br />-    @ no__t-1blank @ no__t:信頼されたドメインをテストします。<br />-    @ no__t @ no__t-2Domain:ドメインコントローラーの参照。<br />-    @ no__t-1 @ no__t-2Domain @ no__t-3SYSvol:SYSvol 参照。<br />-    @ no__t-1 @ no__t-2Domain @ no__t-3NETLOGON:NETLOGON の紹介。<br />-    @ no__t-1 @ no__t @ no__t @ no__t-5: 次のようになります。名前空間のルート参照。<br />-    @ no__t-1 @ no__t @ no__t @ no__t-5 @ no__t-6 @ no__t のようになります。DFS フォルダー \(link @ no__t の紹介。|  
|\/Full|ドメインおよびルートの参照にのみ適用されます。 レジストリと active directory ドメインサービス \(AD DS @ no__t-1 の間のサイトの関連付け情報の整合性を確認します。|  
  
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
  

