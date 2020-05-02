---
title: active
description: ベーシックディスク上のアクティブなコマンドの参照トピックは、パーティションをアクティブとしてマークします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 997c57b93434738c87396812c9b5e5b12d7a8e89
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719012"
---
# <a name="active"></a>active

ベーシック ディスクで、フォーカスのあるパーティションをアクティブとしてマークします。 アクティブとしてマークできるのはパーティションのみです。 この操作を正常に実行するには、パーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してパーティションを選択し、それにフォーカスを移動します。

> [!CAUTION]
> DiskPart は、基本入出力システム (BIOS) または拡張ファームウェアインターフェイス (EFI) に対してのみ、パーティションまたはボリュームが有効なシステムパーティションまたはシステムボリュームであること、およびオペレーティングシステムのスタートアップファイルを含むことができることを通知します。 DiskPart では、パーティションの内容を確認できません。 パーティションを誤ってアクティブとしてマークし、オペレーティングシステムのスタートアップファイルが含まれていない場合は、コンピューターが起動しないことがあります。

## <a name="syntax"></a>構文

```
active
```

## <a name="examples"></a>例

アクティブパーティションとしてフォーカスを持つパーティションをマークするには、次のように入力します。

```
active
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [パーティションの選択コマンド](select-partition.md)
