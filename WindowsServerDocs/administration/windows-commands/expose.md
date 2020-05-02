---
title: さらす
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 500dc5cfcd5e2bba4cfbc3cb5ef81a9065ea53cf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725678"
---
# <a name="expose"></a>さらす



は、ドライブ文字、共有、またはマウントポイントとして、永続的なシャドウコピーを公開します。



## <a name="syntax"></a>構文

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|ShadowID|公開するシャドウコピーのシャドウ ID を指定します。|
|\<ドライブ: >|指定されたシャドウコピーをドライブ文字として公開します (例: P:)。|
|\<共有>|指定されたシャドウコピーを共有に公開します\\ \\( *MachineName*\)など)。|
|\<マウントポイント>|指定されたシャドウコピーをマウントポイントに公開し\)ます (例、c:\ シャドウコピー。|

## <a name="remarks"></a>Remarks

-   *ShadowID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

## <a name="examples"></a>例

VSS_SHADOW_1 環境変数に関連付けられている永続的なシャドウコピーをドライブ X として公開するには、次のように入力します。
```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)