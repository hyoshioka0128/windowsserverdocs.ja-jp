---
title: ksetup:changepassword
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f629c6c7930777583df38f5af900ed380ec60f9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878533"
---
# <a name="ksetupchangepassword"></a>ksetup:changepassword



ログオン ユーザーのパスワードを変更するのにには、キー配布センター (KDC) のパスワード (kpasswd) 値を使用します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /changepassword <OldPasswd> <NewPasswd>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<OldPasswd>|ログオンしたユーザーの既存のパスワードを示しています。|
|\<NewPasswd>|ログオンしたユーザーの新しいパスワードを状態します。|

## <a name="remarks"></a>注釈

このコマンドは、ログオン ユーザーのパスワードを変更するのに KDC (kpasswd) のパスワードの値を使用します。 Kpasswd 場合設定を実行して、出力が表示されます、 **ksetup/dumpstate**コマンド。

ユーザーの新しいパスワードには、このコンピューターに設定されているすべてのパスワード要件を満たす必要があります。

現在のドメイン ユーザー アカウントが見つからない場合は、システムからユーザー アカウントが存在するドメイン名の指定を求められます。

次回ログオン時のパスワードの変更を強制するには、ユーザーは新しいパスワードを求めるために、このコマンドは、アスタリスク (*) を使用できます。

コマンドの出力は、成功または失敗のステータスを通知します。

## <a name="BKMK_Examples"></a>例

このドメインでは、このコンピューターに現在ログオンしているユーザーのパスワードを変更します。
```
ksetup /changepassword Pas$w0rd Pa$$w0rd
```
現在、Contoso ドメインにログオンしたユーザーのパスワードを変更します。
```
ksetup /domain CONTOSO /changepassword Pas$w0rd Pa$$w0rd
```
[次へ] のログオン時にパスワードを変更する現在ログオンしてユーザーを強制します。
```
ksetup /changepassword Pas$w0rd *
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)