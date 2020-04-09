---
title: create partition efi
description: Windows コマンドのトピック create partition efi では、Itanium ベースのコンピューター上の GUID パーティションテーブル (gpt) ディスクに拡張ファームウェアインターフェイス (EFI) システムパーティションが作成されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c61f103fc719c8144e942f64172e3be554a414
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847045"
---
# <a name="create-partition-efi"></a>create partition efi

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Itanium ベースのコンピューターでは、によって、GUID パーティションテーブル (gpt) ディスクに拡張ファームウェアインターフェイス (EFI) システムパーティションが作成されます。

## <a name="syntax"></a>構文  
  
```  
create partition efi [size=<n>] [offset=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                             説明                                                                                              |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  サイズ\=<n>  |                         パーティションのサイズ (mb 単位 \(MB\)。 サイズが指定されていない場合は、現在の領域に空き領域がなくなるまで、パーティションは続行されます。                         |
| オフセット\=<n> |             パーティションが作成されるオフセット (kb \(KB\))。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最初のディスクエクステントに配置されます。              |
|    noerr    | スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |
  
## <a name="remarks"></a>コメント  
  
-   パーティションが作成された後、フォーカスが新しいパーティションに与えられます。  
  
-   この操作を成功させるには、gpt ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。  
  
## <a name="examples"></a><a name=BKMK_examples></a>例  
選択したディスクに 1000 mb の EFI パーティションを作成するには、次のように入力します。  
  
```  
create partition efi size=1000  
```  
  
## <a name="additional-references"></a>その他の参照情報  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

