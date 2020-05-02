---
title: create volume simple
description: 指定されたダイナミックディスクにシンプルボリュームを作成する create volume simple のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: da0f208d-7fda-471a-9db2-5de5ba5207c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f92bd9cf92dea258c6a49dd4cf75c4aae357c88e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716931"
---
# <a name="create-volume-simple"></a>create volume simple

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたダイナミックディスクにシンプルボリュームを作成します。  
  
> [!IMPORTANT]  
> Windows Vista では、この DiskPart コマンドは、Windows Vista Ultimate、Windows Vista Enterprise、および Windows Vista Business edition でのみ使用できます。
  
## <a name="syntax"></a>構文  
  
```  
create volume simple [size=<n>] [disk=<n>] [align=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
| パラメーター  |                                                                                                                            [説明]                                                                                                                            |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 幅\=<n>  |                                                                  ボリュームのサイズ ( \(mb 単位)。\) サイズを指定しないと、新しいボリュームはディスク上の残りの空き領域を占有します。                                                                   |
| ディスク\=<n>  |                                                                                ボリュームが作成されるダイナミックディスク。 ディスクが指定されていない場合は、現在のディスクが使用されます。                                                                                |
| 位置\=<n> | すべてのボリュームエクステントを最も近い配置境界に配置します。 通常、パフォーマンスを向上させるため\(に\) 、ハードウェア RAID 論理ユニット番号 LUN アレイと共に使用します。 *n*は、ディスクの先頭\(から\)最も近いアラインメント境界までのキロバイト kb 数です。 |
|   noerr    |                               スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                |
  
## <a name="remarks"></a>Remarks  
  
-   ボリュームを作成すると、フォーカスは自動的に新しいボリュームに移動します。  
  
## <a name="examples"></a>例  
サイズが 1000 mb のボリュームを作成するには、ディスク1で次のように入力します。  
  
```  
create volume simple size=1000 disk=1  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

