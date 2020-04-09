---
title: さらす
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55cc7a292b81977a346f3f078a3b5623243ea46c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844805"
---
# <a name="expose"></a>さらす



は、ドライブ文字、共有、またはマウントポイントとして、永続的なシャドウコピーを公開します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ShadowID|公開するシャドウコピーのシャドウ ID を指定します。|
|\<ドライブ: >|指定されたシャドウコピーをドライブ文字として公開します (例: P:)。|
|\<共有 >|指定されたシャドウコピーを共有に公開します (たとえば、\\\\*MachineName*\)です。|
|マウントポイントの \<>|指定されたシャドウコピーをマウントポイントに公開します (たとえば、C:\ シャドウ\)。|

## <a name="remarks"></a>コメント

-   *ShadowID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

## <a name="examples"></a><a name=BKMK_examples></a>例

VSS_SHADOW_1 環境変数に関連付けられている永続的なシャドウコピーをドライブ X として公開するには、次のように入力します。
```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)