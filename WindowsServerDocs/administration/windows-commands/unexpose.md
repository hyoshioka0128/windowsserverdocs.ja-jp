---
title: を非公開
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58dc7d0f-52e9-4587-9487-d3b4c3e52640
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e10126739ef82b060e271e9b804a77658b5ec82
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392267"
---
# <a name="unexpose"></a>を非公開



**[公開]** コマンドを使用して公開されたシャドウコピーを公開しません。 公開されたシャドウコピーは、シャドウ ID、ドライブ文字、共有、またはマウントポイントによって指定できます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
unexpose {<ShadowID> | <Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowID >|指定したシャドウ ID によって指定されたシャドウコピーを非公開にします。|
|\<ドライブ: >|指定したドライブ文字 (ドライブ P など) に関連付けられているシャドウコピーを非公開にします。|
|\<共有 >|指定した共有に関連付けられているシャドウコピーを公開しないようにします (たとえば、\\\\*MachineName*\)。|
|マウントポイントの \<>|指定されたマウントポイントに関連付けられているシャドウコピーを公開しないようにします (たとえば、C:\ シャドウ\)します。|

## <a name="remarks"></a>注釈

-   *ShadowID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

## <a name="BKMK_examples"></a>例

ドライブ P に関連付けられたシャドウコピーを公開しないようにするには、次のように入力します。
```
unexpose P:
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)