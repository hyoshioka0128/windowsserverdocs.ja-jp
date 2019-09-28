---
title: 'ksetup: changepassword'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51be9e71c2b290e6346d23144543e0eec29f9d07
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375180"
---
# <a name="ksetupchangepassword"></a>ksetup: changepassword



では、キー配布センター (KDC) のパスワード (kpasswd) 値を使用して、ログオンしているユーザーのパスワードを変更します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<OldPasswd >|ログオンしているユーザーの既存のパスワードを示します。|
|\<NewPasswd >|ログオンしているユーザーの新しいパスワードを示します。|

## <a name="remarks"></a>コメント

このコマンドは、KDC パスワード (kpasswd) の値を使用して、ログオンしているユーザーのパスワードを変更します。 Kpasswd が設定されている場合は、 **ksetup/dumpstate**コマンドを実行して出力に表示されます。

ユーザーの新しいパスワードは、このコンピューターに設定されているすべてのパスワード要件を満たしている必要があります。

現在のドメインにユーザーアカウントが見つからない場合は、ユーザーアカウントが存在するドメイン名を入力するように求められます。

次回ログオン時にパスワードの変更を強制する場合は、このコマンドでアスタリスク (*) を使用できるので、ユーザーは新しいパスワードの入力を求められます。

コマンドの出力によって、成功または失敗の状態が通知されます。

## <a name="BKMK_Examples"></a>例

このドメインのこのコンピューターに現在ログオンしているユーザーのパスワードを変更します:
```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```
Contoso ドメインで現在ログオンしているユーザーのパスワードを変更します。
```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```
現在ログオンしているユーザーに対して、次回ログオン時にパスワードの変更を強制します。
```
ksetup /changepassword Pas$w0rd *
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)