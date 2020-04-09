---
title: create volume simple
description: Create volume simple の Windows コマンドに関するトピック。指定されたダイナミックディスクにシンプルボリュームを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45c707a92692c5531a0e33c9537705558f2ac309
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846895"
---
# <a name="create-volume-simple"></a>create volume simple

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたダイナミックディスクにシンプルボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows Vista では、この DiskPart コマンドは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition でのみ使用できます。
  
## <a name="syntax"></a>構文  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                                                            説明                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| サイズ\=<n>  |                                                                  ボリュームのサイズ (メガバイト \(MB\))。 サイズを指定しないと、新しいボリュームはディスク上の残りの空き領域を占有します。                                                                   |
| ディスク\=<n>  |                                                                                ボリュームが作成されるダイナミックディスク。 ディスクが指定されていない場合は、現在のディスクが使用されます。                                                                                |
| \=<n> に揃える | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるために、LUN\) 配列 \(ハードウェア RAID 論理ユニット番号と共に使用します。 *n*は、ディスクの先頭から最も近いアラインメント境界までの \(KB\) kb 数です。 |
|   noerr    |                               スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                |
  
## <a name="remarks"></a>コメント  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
サイズが 1000 mb のボリュームを作成するには、ディスク1で次のように入力します。  
  
```  
create volume simple size=1000 disk=1  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

