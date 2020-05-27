---
title: ksetup changepassword
description: Ksetup changepassword コマンドのリファレンストピックです。このコマンドは、キー配布センター (KDC) パスワード (kpasswd) 値を使用して、ログオンしているユーザーのパスワードを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 283078e7-a88f-4875-90e6-f8605e6b7ea7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c1ed9d9b611a7911c4a22c7ca803b480f52f323
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817982"
---
# <a name="ksetup-changepassword"></a>ksetup changepassword

では、キー配布センター (KDC) のパスワード (kpasswd) 値を使用して、ログオンしているユーザーのパスワードを変更します。 コマンドの出力によって、成功または失敗の状態が通知されます。

コマンドを実行して出力を表示することによって、 **kpasswd**が設定されているかどうかを確認でき `ksetup /dumpstate` ます。


## <a name="syntax"></a>構文

```
ksetup /changepassword <oldpassword> <newpassword>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<oldpassword>` | ログオンしているユーザーの既存のパスワードを指定します。 |
| `<newpassword>` | ログオンしているユーザーの新しいパスワードを指定します。 このパスワードは、このコンピューターで設定されているすべてのパスワード要件を満たしている必要があります。 |

#### <a name="remarks"></a>注釈

- ユーザーアカウントが現在のドメインに見つからない場合は、ユーザーアカウントが存在するドメイン名を入力するように求められます。

- 次回ログオン時にパスワードの変更を強制する場合は、このコマンドでアスタリスク (*) を使用できるので、ユーザーは新しいパスワードの入力を求められます。

-

### <a name="examples"></a>例

このドメインのこのコンピューターに現在ログオンしているユーザーのパスワードを変更するには、次のように入力します。

```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```

Contoso ドメインで現在ログオンしているユーザーのパスワードを変更するには、次のように入力します。

```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```

現在ログオンしているユーザーに対して、次回ログオン時にパスワードの変更を強制するには、次のように入力します。

```
ksetup /changepassword Pas$w0rd *
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup dumpstate コマンド](ksetup-dumpstate.md)

- [ksetup addkpasswd コマンド](ksetup-addkpasswd.md)

- [ksetup delkpasswd コマンド](ksetup-delkpasswd.md)

- [ksetup dumpstate コマンド](ksetup-dumpstate.md)
