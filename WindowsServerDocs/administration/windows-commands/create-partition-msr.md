---
title: create partition msr
description: Create partition msr のリファレンストピックでは、GUID パーティションテーブル (gpt) ディスクに Microsoft 予約 (MSR) パーティションを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 04fba033-23cb-4521-bd5d-db96131f2e73
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 964f57b08a23867c01d3e90e9b8283c7b4fff6e5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719217"
---
# <a name="create-partition-msr"></a>create partition msr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

GUID パーティションテーブル (gpt) ディスクに Microsoft 予約 (MSR) パーティションを作成します。
  
> [!CAUTION]  
> このコマンドを使用する場合は注意が必要です。 Gpt ディスクには特定のパーティションレイアウトが必要であるため、Microsoft 予約パーティションを作成すると、ディスクが読み取り不能になる可能性があります。
  
## <a name="syntax"></a>構文  
  
```  
create partition msr [size=<n>] [offset=<n>] [noerr]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|  パラメーター  |                                                                                                                         [説明]                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  幅\=<n>  |               パーティションのサイズ ( \(mb 単位)。\) パーティションは、によっ<n>て指定された数以上、バイト単位で指定します。 サイズが指定されていない場合は、現在の領域に空き領域がなくなるまで、パーティションは続行されます。               |
| 影\=<n> | パーティションが作成される\(オフセット\)をキロバイト kb 単位で指定します。 オフセットは、使用されるセクターサイズを完全に埋めるために切り上げられます。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最初のディスクエクステントに配置されます。 |
|    noerr    |                            スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                             |
  
## <a name="remarks"></a>Remarks  
  
-   Windows オペレーティングシステムの起動に使用される gpt ディスクでは、拡張ファームウェアインターフェイス\(EFI\)システムパーティションがディスク上の最初のパーティションになり、その後に Microsoft 予約パーティションが続きます。 データ記憶域にのみ使用される gpt ディスクには、EFI システムパーティションがありません。この場合、Microsoft 予約パーティションが最初のパーティションになります。  
  
-   Windows では、Microsoft 予約パーティションはマウントされません。 このパーティションにはデータを保存できません。また、このパーティションは削除できません。  
  
-   Microsoft 予約パーティションは、すべての gpt ディスクに必要です。 このパーティションのサイズは、gpt ディスクの合計サイズによって異なります。 Microsoft 予約パーティションを作成するには、gpt ディスクのサイズが 32 MB 以上である必要があります。  
  
-   この操作を成功させるには、ベーシック gpt ディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用して、ベーシック gpt ディスクを選択し、それにフォーカスを移動します。  
  
## <a name="examples"></a>例  
サイズが 1000 mb の Microsoft 予約パーティションを作成するには、次のように入力します。  
  
```  
create partition msr size=1000  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
  

  

