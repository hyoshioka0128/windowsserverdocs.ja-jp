---
title: gpt
description: Gpt コマンドの参照記事。フォーカスのあるパーティションに gpt 属性を割り当てます。
ms.topic: article
ms.assetid: 1d6f9029-807f-4420-a336-36669b5361bc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 561bc4a11580a45452ac71cffddee1c58e48cf86
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888553"
---
# <a name="gpt"></a>gpt

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

基本的な GUID パーティションテーブル (gpt) ディスクでは、このコマンドを実行すると、フォーカスがあるパーティションに gpt 属性が割り当てられます。 Gpt パーティション属性は、パーティションの使用に関する追加情報を提供します。 いくつかの属性は、パーティションの種類を表す GUID に固有です。

この操作を成功させるには、基本 gpt パーティションを選択する必要があります。 [[パーティションの選択] コマンド](select-partition.md)を使用して、基本的な gpt パーティションを選択し、それにフォーカスを移動します。

> [!CAUTION]
> Gpt 属性を変更すると、基本データボリュームにドライブ文字が割り当てられなかったり、ファイルシステムがマウントされないようになったりする可能性があります。 Gpt の属性を変更しないことを強くお勧めします。これは、相手先ブランド供給 (OEM) または gpt ディスクの使用経験がある IT プロフェッショナルでない限りです。

## <a name="syntax"></a>構文

```
gpt attributes=<n>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 属性 =`<n>` | フォーカスのあるパーティションに適用する属性の値を指定します。 Gpt 属性フィールドは、2つのサブフィールドを含む64ビットフィールドです。 上位フィールドは、パーティション ID との関係でのみ解釈され、下位フィールドは、すべてのパーティション ID に共通です。 許容される値は次のとおりです。<ul><li>**0x0000000000000001** -コンピューターが正常に機能するためにパーティションが必要であることを指定します。</li><li>**0x8000000000000000** -ディスクが別のコンピューターに移動されたとき、またはディスクがコンピューターによって初めて検出されたときに、パーティションが既定でドライブ文字を受け取らないことを指定します。</li><li>**0x4000000000000000** -パーティションのボリュームを非表示にして、マウントマネージャーによって検出されないようにします。</li><li>**0x2000000000000000** -パーティションが別のパーティションのシャドウコピーであることを指定します。</li><li>**0x1000000000000000** -パーティションが読み取り専用であることを指定します。 この属性は、ボリュームが書き込まれないようにします。</li></ul><p>これらの属性の詳細については、「 [Create_PARTITION_PARAMETERS Structure](/windows/win32/api/vds/ns-vds-create_partition_parameters)」の「attributes」セクションを参照してください。 |

#### <a name="remarks"></a>Remarks

- EFI システムパーティションには、オペレーティングシステムを起動するために必要なバイナリのみが含まれています。 これにより、OEM バイナリまたはオペレーティングシステム固有のバイナリを他のパーティションに簡単に配置できます。

### <a name="examples"></a>例

Gpt ディスクの移動中に、コンピューターがフォーカスのあるパーティションにドライブ文字を自動的に割り当てないようにするには、次のように入力します。

```
gpt attributes=0x8000000000000000
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [パーティションの選択コマンド](select-partition.md)

- [create_PARTITION_PARAMETERS 構造体](/windows/win32/api/vds/ns-vds-create_partition_parameters)
