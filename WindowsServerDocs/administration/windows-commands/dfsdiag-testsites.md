---
title: dfsdiag TestSites
description: Dfs diag TestSites の Windows コマンドトピックでは、名前空間サーバーまたはフォルダ (リンク) のターゲットとして機能するサーバーがすべてのドメインコントローラ上で同じサイトの関連付けを持つことを確認することで、active directory ドメインサービス (AD DS) サイトの構成を確認します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80cc9095748dafb030b204130bfa2ccb61ec69ea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846225"
---
# <a name="dfsdiag-testsites"></a>dfsdiag TestSites

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

名前空間サーバーまたはフォルダー (リンク) のターゲットとして機能するサーバーがすべてのドメインコントローラー上で同じサイトの関連付けを持つことを確認して、active directory ドメインサービス (AD DS) サイトの構成を確認します。

## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
#### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/マシン:<server name>|サイトの関連付けを確認するサーバーの名前。|  
|\/DFSpath:<namespace root or DFS folder>|サイトの関連付けを検証するターゲットを持つ名前空間のルートまたは分散ファイルシステム (DFS) フォルダー (リンク)。|  
|再帰 \/|指定した名前空間のルートにあるすべてのフォルダーターゲットのサイトの関連付けを列挙し、検証します。|  
|\/完全|AD DS とサーバーのレジストリに同じサイトの関連付け情報が含まれていることを確認します。|  
  
## <a name="examples"></a><a name=BKMK_Examples></a>例  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
 
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

