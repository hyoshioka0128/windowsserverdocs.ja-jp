---
title: active
description: Windows コマンド」のトピック**active** - ベーシック ディスクで、アクティブとしてフォーカスのあるパーティションをマークします。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3a039e0200fb84d446739ac7017556b6c302f4af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868763"
---
# <a name="active"></a>active



ベーシック ディスクで、アクティブとしてフォーカスのあるパーティションをマークします。

> [!CAUTION]
> DiskPart は、パーティションがオペレーティング システムのスタートアップ ファイルを収容できることにのみ確認します。 DiskPart では、パーティションの内容を確認しません。 パーティションをアクティブとして誤ってマークする、オペレーティング システムのスタートアップ ファイルが含まれていない場合は、コンピューターが起動しない可能性があります。

## <a name="syntax"></a>構文

```
active
```

## <a name="remarks"></a>注釈

-   これは、パーティションまたはボリュームが、有効なシステム パーティションまたはシステム ボリュームがある基本入出力システム (BIOS) または拡張ファームウェア インターフェイス (EFI) 通知されます。
-   パーティションのみをアクティブとしてマークすることができます。
-   この操作を成功させるのには、パーティションを選択してください。 使用して、**パーティションを選択**コマンドをパーティションを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

アクティブ パーティションとしてフォーカスのあるパーティションをマークするには、次のように入力します。
```
active
```

#### <a name="additional-references"></a>その他の参照情報

