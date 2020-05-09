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
ms.openlocfilehash: d427e9f96023f8b66f72e3895b30519ab7cd2de1
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993260"
---
# <a name="create-partition-msr"></a>create partition msr

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

GUID パーティションテーブル (gpt) ディスクに Microsoft 予約 (MSR) パーティションを作成します。 Microsoft 予約パーティションは、すべての gpt ディスクに必要です。 このパーティションのサイズは、gpt ディスクの合計サイズによって異なります。 Microsoft 予約パーティションを作成するには、gpt ディスクのサイズが 32 MB 以上である必要があります。

> [!IMPORTANT]
> このコマンドを使用する場合は注意が必要です。 Gpt ディスクには特定のパーティションレイアウトが必要であるため、Microsoft 予約パーティションを作成すると、ディスクが読み取れなくなる可能性があります。
>
> この操作を成功させるには、ベーシック gpt ディスクを選択する必要があります。 [[ディスクの選択](select-disk.md)] コマンドを使用してベーシック gpt ディスクを選択し、それにフォーカスを移動する必要があります。

## <a name="syntax"></a>構文

```
create partition msr [size=<n>] [offset=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | パーティションのサイズ (mb)。 パーティションは、によっ`<n>`て指定された数以上、バイト単位で指定します。 サイズが指定されていない場合は、現在の領域に空き領域がなくなるまで、パーティションは続行されます。 |
| オフセット =`<n>` | パーティションが作成されるオフセットをキロバイト (KB) 単位で指定します。 オフセットは、使用されるセクターサイズを完全に埋めるために切り上げられます。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最初のディスクエクステントに配置されます。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

#### <a name="remarks"></a>Remarks

- Windows オペレーティングシステムの起動に使用される gpt ディスクでは、拡張ファームウェアインターフェイス (EFI) システムパーティションがディスク上の最初のパーティションになり、その後に Microsoft 予約パーティションが続きます。 データ記憶域にのみ使用される gpt ディスクには、EFI システムパーティションがありません。この場合、Microsoft 予約パーティションが最初のパーティションになります。

- Windows は Microsoft 予約パーティションをマウントしません。 このパーティションにはデータを保存できません。また、このパーティションは削除できません。

## <a name="examples"></a>使用例

サイズが 1000 mb の Microsoft 予約パーティションを作成するには、次のように入力します。

```
create partition msr size=1000
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)

- [select disk](select-disk.md)
