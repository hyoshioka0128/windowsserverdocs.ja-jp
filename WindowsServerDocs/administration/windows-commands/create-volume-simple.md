---
title: ボリュームのシンプルな作成
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1afb97c5bdb167eaf6ecfcd34ca3607b7b5a4c71
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378881"
---
# <a name="create-volume-simple"></a>ボリュームのシンプルな作成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたダイナミックディスクにシンプルボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows Vista では、この DiskPart コマンドは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition でのみ使用できます。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                                                            説明                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| サイズ\=<n>  |                                                                  ボリュームのサイズ (メガバイト \(MB\))。 サイズが指定されていない場合、新しいボリュームはディスクの残りの空き領域を占有します。                                                                   |
| disk\=<n>  |                                                                                ボリュームが作成されるダイナミックディスク。 ディスクが指定されていない場合は、現在のディスクが使用されます。                                                                                |
| align\=<n> | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、LUN\) 配列 \(ハードウェア RAID 論理ユニット番号と共に使用します。 *n*は、ディスクの先頭から最も近いアラインメント境界までの \(KB\) kb 数です。 |
|   noerr    |                               スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                |
  
## <a name="remarks"></a>注釈  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移ります。  
  
## <a name="BKMK_examples"></a>例  
サイズが 1000 mb のボリュームを作成するには、ディスク1で次のように入力します。  
  
```  
create volume simple size=1000 disk=1  
```  
  
#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

