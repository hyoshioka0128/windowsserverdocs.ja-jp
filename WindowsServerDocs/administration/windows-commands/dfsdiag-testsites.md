---
title: Dfsdiag TestSites
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6486c79cfa58bb262fd3161ad0801e84185b6629
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873973"
---
# <a name="dfsdiag-testsites"></a>Dfsdiag TestSites

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active directory Domain Services の構成をチェック\(AD DS\)サイトを確認することでそのサーバーの名前空間サーバーまたはフォルダーとして機能する\(リンク\)ターゲットのすべてのドメインと同じサイトの関連性のあります。コント ローラー。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestSites </Machine:<server name>| /DFSpath:<namespace root or DFS folder> [/Recurse]> [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/マシンの場合:<server name>|サイトの関連付けを確認するサーバーの名前。|  
|\/DFSpath:<namespace root or DFS folder>|名前空間のルートまたは分散ファイル システム\(DFS\)フォルダー\(リンク\)サイト関連付けを確認する対象のターゲットを使用します。|  
|\/Recurse|列挙し、指定した名前空間のルートの下のすべてのフォルダー ターゲットのサイトの関連付けを確認します。|  
|\/完全です|AD DS とサーバーのレジストリが、同じサイトの関連付け情報を含めることを確認します。|  
  
## <a name="BKMK_Examples"></a>例  
TBD を入力します。  
  
```  
dfsdiag /TestSites /Machine:MyServer  
```  
  
TBD を入力します。  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace1\Folder1 /Full  
```  
  
TBD を入力します。  
  
```  
dfsdiag /TestSites /DFSpath:\\Contoso.com\Namespace2 /Recurse /Full  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

