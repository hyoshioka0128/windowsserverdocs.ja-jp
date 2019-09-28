---
title: 'ksetup: setcomputerpassword'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1d3742476385eb770c9cb5c798c1f6ab27c74f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374940"
---
# <a name="ksetupsetcomputerpassword"></a>ksetup: setcomputerpassword



ローカルコンピューターのパスワードを設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setcomputerpassword <Password>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<Password >|指定されたパスワードを使用して、ローカルコンピューターのコンピューターアカウントを設定します。</br>パスワードは、管理者特権を持つアカウントを使用してのみ設定できます。 パスワードには、1 ~ 156 の英数字または特殊文字を使用できます。|

## <a name="remarks"></a>コメント

このコマンドは、コンピューターアカウントのみに影響します。

パスワードの変更を有効にするには、コンピューターを再起動する必要があります。

コンピューターアカウントのパスワードは、レジストリまたは**ksetup**コマンドからの出力としては表示されません。

## <a name="BKMK_Examples"></a>例

ローカルコンピューターのコンピューターアカウントのパスワードを IPops897 から IPop $ 897! に変更します。
```
ksetup /setcomputerpassword IPop$897!
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)