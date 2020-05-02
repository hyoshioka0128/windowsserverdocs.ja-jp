---
title: 'ksetup: changepassword'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32c48e896b77043820eea42159e20c089bd69fb8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724725"
---
# <a name="ksetupchangepassword"></a>ksetup: changepassword



では、キー配布センター (KDC) のパスワード (kpasswd) 値を使用して、ログオンしているユーザーのパスワードを変更します。

## <a name="syntax"></a>構文

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<OldPasswd>|ログオンしているユーザーの既存のパスワードを示します。|
|\<NewPasswd>|ログオンしているユーザーの新しいパスワードを示します。|

## <a name="remarks"></a>Remarks

このコマンドは、KDC パスワード (kpasswd) の値を使用して、ログオンしているユーザーのパスワードを変更します。 Kpasswd が設定されている場合は、 **ksetup/dumpstate**コマンドを実行して出力に表示されます。

ユーザーの新しいパスワードは、このコンピューターに設定されているすべてのパスワード要件を満たしている必要があります。

現在のドメインにユーザーアカウントが見つからない場合は、ユーザーアカウントが存在するドメイン名を入力するように求められます。

次回ログオン時にパスワードの変更を強制する場合は、このコマンドでアスタリスク (*) を使用できるので、ユーザーは新しいパスワードの入力を求められます。

コマンドの出力によって、成功または失敗の状態が通知されます。

## <a name="examples"></a>例

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

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)