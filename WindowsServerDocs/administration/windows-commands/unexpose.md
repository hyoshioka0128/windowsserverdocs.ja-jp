---
title: を非公開
description: '[公開] コマンドを使用して公開されたシャドウコピーを非公開にするための Windows コマンドに関するトピック。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2f8bbdb3b810ffbf9332608a016fc3b3e188e9f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832355"
---
# <a name="unexpose"></a>を非公開

**[公開]** コマンドを使用して公開されたシャドウコピーを公開しません。 公開されたシャドウコピーは、シャドウ ID、ドライブ文字、共有、またはマウントポイントによって指定できます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowID >|指定したシャドウ ID によって指定されたシャドウコピーを非公開にします。|
|\<ドライブ: >|指定したドライブ文字 (ドライブ P など) に関連付けられているシャドウコピーを非公開にします。|
|\<共有 >|指定した共有に関連付けられているシャドウコピーを公開しないようにします (たとえば、\\\\*MachineName*\)。|
|マウントポイントの \<>|指定されたマウントポイントに関連付けられているシャドウコピーを公開しないようにします (たとえば、C:\ シャドウ\)します。|

## <a name="remarks"></a>コメント

-   *ShadowID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

## <a name="examples"></a><a name=BKMK_examples></a>例

ドライブ P に関連付けられたシャドウコピーを公開しないようにするには、次のように入力します。
```
unexpose P:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)