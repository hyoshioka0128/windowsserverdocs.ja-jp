---
title: break
description: '**Break_2**の Windows コマンドに関するトピック-VSS からシャドウコピーボリュームの関連付けを解除し、通常のボリュームとしてアクセスできるようにします。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a5789e3442152c705b3197bf1ce5e63dc782a15c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379778"
---
# <a name="break"></a>break



シャドウコピーボリュームを VSS から切り離し、通常のボリュームとしてアクセスできるようにします。 ボリュームには、ドライブ文字 (割り当てられている場合) またはボリューム名を使用してアクセスできます。 パラメーターを指定せずに使用した場合は、コマンドプロンプトに [**ヘルプ] が**表示されます。

> [!NOTE]
> このコマンドは、インポート後のハードウェアシャドウコピーにのみ関連します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
break [writable] <SetID>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|書き込み可能|ボリュームの読み取り/書き込みアクセスを有効にします。|
|\<SetID >|シャドウコピーセットの ID を指定します。|

## <a name="remarks"></a>コメント

-   公開されているボリュームは、既定では読み取り専用です。
-   **Load metadata**コマンドによって環境変数として格納されているシャドウコピー ID のエイリアスは、 *SetID*パラメーターで使用できます。

## <a name="BKMK_examples"></a>例

エイリアス名 Alias1 を使用してシャドウコピーを作成し、オペレーティングシステムで書き込み可能なボリュームとしてアクセスできるようにするには、次のように入力します。
```
break writable %Alias1%
```

> [!NOTE]
> ボリュームへのアクセスは、シャドウコピーされたボリュームを記録せずに、ハードウェアプロバイダーに直接行われます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)