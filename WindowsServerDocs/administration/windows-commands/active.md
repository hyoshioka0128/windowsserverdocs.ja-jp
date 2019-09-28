---
title: active
description: '**アクティブ**なベーシックディスクに関する Windows コマンドのトピックでは、パーティションをアクティブとしてマークします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c926bf9b7a583cf7eaa23166e09e6f0a1599e625
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382848"
---
# <a name="active"></a>active



ベーシックディスクでは、はパーティションをアクティブとしてマークします。

> [!CAUTION]
> DiskPart では、パーティションがオペレーティングシステムのスタートアップファイルを含むことができるかどうかのみが検証されます。 DiskPart では、パーティションの内容は確認されません。 パーティションを誤ってアクティブとしてマークし、オペレーティングシステムのスタートアップファイルが含まれていない場合は、コンピューターが起動しないことがあります。

## <a name="syntax"></a>構文

```
active
```

## <a name="remarks"></a>コメント

-   これにより、パーティションまたはボリュームが有効なシステムパーティションまたはシステムボリュームであることが、基本入出力システム (BIOS) または拡張ファームウェアインターフェイス (EFI) に通知されます。
-   アクティブとしてマークできるのはパーティションのみです。
-   この操作を成功させるには、パーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してパーティションを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

アクティブパーティションとしてフォーカスを持つパーティションをマークするには、次のように入力します。
```
active
```

#### <a name="additional-references"></a>その他の参照情報

