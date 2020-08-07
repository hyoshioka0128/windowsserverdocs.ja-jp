---
title: 中断 (シャドウコピーボリューム)
description: 中断コマンドの参照記事。 VSS からシャドウコピーボリュームの関連付けを解除し、通常のボリュームとしてアクセスできるようにします。
ms.topic: article
ms.assetid: de2b6c95-1c2e-4a43-bec5-341a9014371b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 125f986152d10844bbab5a7b57a1a2ea4080aa3e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880463"
---
# <a name="break-shadow-copy-volume"></a>中断 (シャドウコピーボリューム)

シャドウコピーボリュームを VSS から切り離し、通常のボリュームとしてアクセスできるようにします。 ボリュームには、ドライブ文字 (割り当てられている場合) またはボリューム名を使用してアクセスできます。 パラメーターを指定せずに使用した場合は、コマンドプロンプトに [**ヘルプ] が**表示されます。

> [!NOTE]
> このコマンドは、インポート後のハードウェアシャドウコピーにのみ関連します。
>
> 公開されているボリュームは、既定では読み取り専用です。 ボリュームへのアクセスは、シャドウコピーされたボリュームを記録せずに、ハードウェアプロバイダーに直接行われます。

## <a name="syntax"></a>構文

```
break [writable] <setid>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 書き込み可能 | ボリュームの読み取り/書き込みアクセスを有効にします。 |
| \<setid> | シャドウコピーセットの ID を指定します。 **Load metadata**コマンドによって環境変数として格納されているシャドウコピー ID のエイリアスは、 *SetID*パラメーターで使用できます。 |

## <a name="examples"></a>例

エイリアス名 Alias1 を使用してシャドウコピーを作成するには、オペレーティングシステムで書き込み可能なボリュームとしてアクセス可能である必要があります。

```
break writable %Alias1%
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)