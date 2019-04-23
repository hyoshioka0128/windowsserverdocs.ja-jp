---
title: 公開
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51cc744bc2b61862ed05ca2e7d0aaa8f70d38692
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886663"
---
# <a name="expose"></a>公開



ドライブ文字、共有、またはマウント ポイントとして永続的なシャドウ コピーを公開します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ShadowID|公開するシャドウ コピーのシャドウ ID を指定します。|
|\<ドライブ: >|ドライブ文字 (たとえば、p:) として指定したシャドウ コピーを公開します。|
|\<Share>|共有にある指定したシャドウ コピーを公開します (たとえば、 \\ \\ *MachineName*\)します。|
|\<MountPoint>|マウント ポイントを指定したシャドウ コピーを公開します (たとえば、C:\shadowcopy\)します。|

## <a name="remarks"></a>注釈

-   既存のエイリアスまたは環境変数の代わりに使用できます*ShadowID*します。 使用**追加**パラメーターに既存の別名を参照してください。

## <a name="BKMK_examples"></a>例

ドライブ X として VSS_SHADOW_1 環境変数に関連付けられた永続的なシャドウ コピーを公開するには、次のように入力します。
```
expose %vss_shadow_1% x:
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)