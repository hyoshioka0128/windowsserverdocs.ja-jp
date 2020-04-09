---
title: 'ksetup: setcomputerpassword'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e65ea6e935d9fde9c23842755c36e418928dec7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841375"
---
# <a name="ksetupsetcomputerpassword"></a>ksetup: setcomputerpassword



ローカルコンピューターのパスワードを設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setcomputerpassword <Password>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<パスワード >|指定されたパスワードを使用して、ローカルコンピューターのコンピューターアカウントを設定します。</br>パスワードは、管理者特権を持つアカウントを使用してのみ設定できます。 パスワードには、1 ~ 156 の英数字または特殊文字を使用できます。|

## <a name="remarks"></a>コメント

このコマンドは、コンピューターアカウントのみに影響します。

パスワードの変更を有効にするには、コンピューターを再起動する必要があります。

コンピューターアカウントのパスワードは、レジストリまたは**ksetup**コマンドからの出力としては表示されません。

## <a name="examples"></a><a name=BKMK_Examples></a>例

ローカルコンピューターのコンピューターアカウントのパスワードを IPops897 から IPop $ 897! に変更します。
```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)