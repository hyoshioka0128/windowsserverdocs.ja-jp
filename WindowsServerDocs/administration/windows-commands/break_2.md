---
title: break
description: Windows コマンドに関するトピックでは、シャドウコピーボリュームを VSS から切り離し、通常のボリュームとしてアクセスできるようにする break_2 について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6683c44c84f4baae5f016f7df62d5bd6591cff70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848255"
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

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|書き込み可能|ボリュームの読み取り/書き込みアクセスを有効にします。|
|\<SetID >|シャドウコピーセットの ID を指定します。|

## <a name="remarks"></a>コメント

-   公開されているボリュームは、既定では読み取り専用です。
-   **Load metadata**コマンドによって環境変数として格納されているシャドウコピー ID のエイリアスは、 *SetID*パラメーターで使用できます。

## <a name="examples"></a><a name=BKMK_examples></a>例

エイリアス名 Alias1 を使用してシャドウコピーを作成し、オペレーティングシステムで書き込み可能なボリュームとしてアクセスできるようにするには、次のように入力します。
```
break writable %Alias1%
```

> [!NOTE]
> ボリュームへのアクセスは、シャドウコピーされたボリュームを記録せずに、ハードウェアプロバイダーに直接行われます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)