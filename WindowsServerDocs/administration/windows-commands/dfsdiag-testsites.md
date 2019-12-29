---
title: dfsdiag TestSites
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39a0d415-7eb7-4a26-861b-7ff00c45dcda
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af72da64dd20d4b37824355a494cb8f97f597b28
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378381"
---
# <a name="dfsdiag-testsites"></a>dfsdiag TestSites

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active directory ドメインサービス \(AD DS\) サイトの構成を確認します。これは、名前空間のサーバーまたはフォルダーとして機能するサーバーが、\) ターゲットをリンクする \(、すべてのドメインコントローラーで同じサイトの関連付けを持つことを確認します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/マシン:<server name>|サイトの関連付けを確認するサーバーの名前。|  
|\/DFSpath:<namespace root or DFS folder>|名前空間のルートまたは分散ファイルシステム \(DFS\) フォルダー \(リンク\)、サイトの関連付けを確認するターゲット。|  
|再帰 \/|指定した名前空間のルートにあるすべてのフォルダーターゲットのサイトの関連付けを列挙し、検証します。|  
|\/完全|AD DS とサーバーのレジストリに同じサイトの関連付け情報が含まれていることを確認します。|  
  
## <a name="BKMK_Examples"></a>例  
次のように入力します。  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
  
次のように入力します。  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
次のように入力します。  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>その他の参照情報  
  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

