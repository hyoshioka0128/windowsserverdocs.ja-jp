---
title: create partition primary
description: Create partition primary コマンドの参照記事。フォーカスがあるベーシックディスク上にプライマリパーティションを作成します。
ms.topic: article
ms.assetid: 6d652d8e-3935-4a91-8ced-b17c0e7937be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5e2869729f56fd09abebb650526ea4f07c86b21
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879871"
---
# <a name="create-partition-primary"></a>create partition primary

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるベーシックディスク上にプライマリパーティションを作成します。 パーティションを作成すると、フォーカスは自動的に新しいパーティションに移動します。

> [!IMPORTANT]
> この操作を成功させるには、ベーシックディスクを選択する必要があります。 [[ディスクの選択](select-disk.md)] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動する必要があります。

## <a name="syntax"></a>構文

```
create partition primary [size=<n>] [offset=<n>] [id={ <byte> | <guid> }] [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | パーティションのサイズ (MB 単位) を指定します。 サイズを指定しないと、パーティションは現在の未割り当て領域いっぱいまで割り当てられます。 |
| オフセット =`<n>` | パーティションが作成されるオフセット (kb 単位)。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最大のディスクエクステントの先頭から開始されます。 |
| align =`<n>` | すべてのパーティションエクステントを最も近いアラインメント境界に配置します。 通常、パフォーマンスを向上させるために、ハードウェア RAID 論理ユニット番号 (LUN) アレイと共に使用します。 `<n>`ディスクの先頭から最も近いアラインメント境界までのキロバイト (KB) 数を指定します。 |
| id = { `<byte>  | <guid>` } | パーティションの種類を指定します。 このパラメーターは、相手先ブランド供給の製造元 (OEM) のみを対象としています。 このパラメーターでは、任意のパーティションの種類のバイトまたは GUID を指定できます。 DiskPart は、16進形式または GUID のバイトであることを除いて、パーティションの種類が有効かどうかをチェックしません。 **注意:** このパラメーターを使用してパーティションを作成すると、コンピューターが失敗するか、起動できなくなる可能性があります。 OEM または gpt ディスクの使用経験がある IT プロフェッショナルでない限り、このパラメーターを使用して gpt ディスクにパーティションを作成しないでください。 代わりに、gpt ディスク上にプライマリパーティションを作成するには、常に[create partition efi](create-partition-efi.md)コマンドを使用して efi システムパーティションを作成し、 [create partition msr](create-partition-msr.md)コマンドを使用して Microsoft 予約パーティションを作成し、[パーティションプライマリ](create-partition-primary.md)を作成し `id={ <byte>  | <guid>` ます。<p>**マスターブートレコード (MBR) ディスクの**場合、パーティションには、16進形式のパーティションの種類のバイトを指定する必要があります。 このパラメーターが指定されていない場合、コマンドは `0x06` 、ファイルシステムがインストールされていないことを指定する型のパーティションを作成します。 以下に例を示します。<ul><li>**LDM データパーティション:** 0x42</li><li>**復旧パーティション:** 0x27</li><li>認識された**OEM パーティション:** 0x12、0X84、0Xde、0Xfe、0xde</li></ul><p>**Guid パーティションテーブル (gpt) ディスクの**場合、作成するパーティションのパーティションの種類の guid を指定できます。 認識された Guid は次のとおりです。<ul><li>**EFI システムパーティション:** c12a7328-f81f-11d2-ba4b-00a0c93ec93b</li><li>**Microsoft 予約パーティション:** e3c9e316-0b5c-4db8-817d-f92df00215ae</li><li>**基本データパーティション:** ebd0a0a2-b9e5-4433-87c0-68b6b72699c7</li><li>**LDM メタデータパーティション (ダイナミックディスク):** 5808c8aa-7e8f-42e0-85d2-e1e90434cfb3</li><li>**LDM データパーティション (ダイナミックディスク):** af9b60a0-1431-4f62-bc68-3311714a69ad</li><li>**復旧パーティション:** de94bba4-06d1-4d40-a16a-bfd50179d6ac<p>このパラメーターが gpt ディスクに指定されていない場合は、基本的なデータパーティションが作成されます。</li></ul> |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 noerr パラメーターを省略した場合、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

サイズが 1000 mb のプライマリパーティションを作成するには、次のように入力します。

```
create partition primary size=1000
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [assign コマンド](assign.md)

- [create コマンド](create.md)

- [select disk](select-disk.md)
