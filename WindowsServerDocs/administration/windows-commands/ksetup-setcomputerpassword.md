---
title: ksetup:setcomputerpassword
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0679bb9ee429e05c7679411c5493bd21b530ef8e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831543"
---
# <a name="ksetupsetcomputerpassword"></a>ksetup:setcomputerpassword



ローカル コンピューターのパスワードを設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setcomputerpassword <Password>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<パスワード >|指定したパスワードを使用すると、ローカル コンピューターのコンピューター アカウントを設定します。</br>パスワードは、管理者特権を持つアカウントを使用してのみ設定できます。 パスワードには、1 ~ 156 の英数字または特殊文字を指定できます。|

## <a name="remarks"></a>注釈

このコマンドでは、コンピューター アカウントのみに影響します。

パスワードの変更を有効にするには、コンピューターを再起動する必要があります。

レジストリまたはからの出力として、コンピューター アカウントのパスワードは表示されませんが、 **ksetup**コマンド。

## <a name="BKMK_Examples"></a>例

IPops897 から IPop ドル 897 にローカル コンピューターのコンピューター アカウントのパスワードを変更しました。
```
ksetup /setcomputerpassword IPop$897!
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)