---
title: break
description: Windows コマンド」のトピック**break_2** - VSS からシャドウ コピー ボリュームの関連付けを解除し、通常のボリュームとしてアクセスできるようにします。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 49516539ae603e2c93b3fc395c77786be790d663
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886333"
---
# <a name="break"></a>break



VSS からシャドウ コピー ボリュームの関連付けを解除し、通常のボリュームとしてアクセスできるようにします。 ボリュームにはドライブ文字 (割り当て場合) またはボリュームの名前を使用してアクセスできます。 パラメーターを指定せずに使用されている場合**break**コマンド プロンプトでヘルプを表示します。

> [!NOTE]
> このコマンドは、インポートした後にハードウェアのシャドウ コピーに対してのみ適用されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
break [writable] <SetID>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[書き込み]|により読み取り/書き込みボリュームにアクセスします。|
|\<SetID>|シャドウ コピー セットの ID を指定します。|

## <a name="remarks"></a>注釈

-   シャドウ コピーから、発生するように、公開されているボリュームとは、既定では読み取り専用です。
-   環境変数として格納されているシャドウ コピー ID のエイリアス、**メタデータの読み込み**コマンドで使用できる、 *SetID*パラメーター。

## <a name="BKMK_examples"></a>例

オペレーティング システムでの書き込み可能なボリュームとしてアクセスできるように Alias1 エイリアス名を使用してコピーをシャドウするために、次のように入力します。
```
break writable %Alias1%
```

> [!NOTE]
> ボリュームへのアクセスは、ボリューム シャドウ コピーになったの記録を行わず、ハードウェア プロバイダーに対して直接行われます。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)