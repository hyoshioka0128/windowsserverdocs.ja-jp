---
title: create partition efi
description: Create partition efi コマンドのリファレンストピックでは、Itanium ベースのコンピューター上の GUID パーティションテーブル (gpt) ディスクに拡張ファームウェアインターフェイス (EFI) システムパーティションを作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cfc1fca-6515-4a4d-bfae-615fa8045ea9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c314d756bebd0d0ec2ed9c844f714f395d04c6b
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993294"
---
# <a name="create-partition-efi"></a>create partition efi

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Itanium ベースのコンピューター上の GUID パーティションテーブル (gpt) ディスクに、拡張ファームウェアインターフェイス (EFI) システムパーティションを作成します。 パーティションが作成されると、新しいパーティションにフォーカスが割り当てられます。

>[!NOTE]
> この操作を成功させるには、gpt ディスクを選択する必要があります。 使用して、 [select ディスク](select-disk.md) コマンド ディスクを選択し、それにフォーカスをします。

## <a name="syntax"></a>構文

```
create partition efi [size=<n>] [offset=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| サイズ =`<n>` | パーティションのサイズ (mb)。 サイズが指定されていない場合は、現在の領域に空き領域がなくなるまで、パーティションは続行されます。 |
| オフセット =`<n>` | パーティションが作成されるオフセット (kb 単位)。 オフセットが指定されていない場合、パーティションは、それを保持するのに十分な大きさの最初のディスクエクステントに配置されます。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

#### <a name="remarks"></a>Remarks

- **Create**コマンドを使用する前に、[**ボリュームの追加**] コマンドでボリュームを少なくとも1つ追加する必要があります。

- **Create**コマンドを実行した後、 **exec**コマンドを使用して、シャドウコピーからバックアップ用の複製スクリプトを実行できます。

- [**バックアップの開始**] コマンドを使用すると、コピーバックアップではなく完全バックアップを指定できます。

## <a name="examples"></a>使用例

選択したディスクに 1000 mb の EFI パーティションを作成するには、次のように入力します。

```
create partition efi size=1000
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [create コマンド](create.md)

- [select disk](select-disk.md)
