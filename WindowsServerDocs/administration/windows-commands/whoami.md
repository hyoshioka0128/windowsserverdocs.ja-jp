---
title: whoami
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3f4d5c-f1f5-4429-b602-afad2b3488bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6844ba001c2ebd7407b77f97204069a48a1b595b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840153"
---
# <a name="whoami"></a>whoami



現在、ローカル システムにログオンしたユーザーのユーザー、グループおよび権限の情報が表示されます。 パラメーターを指定せずに使用されている場合**whoami**現在のドメインとユーザー名が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
whoami [/upn | /fqdn | /logonid]
whoami {[/user] [/groups] [/priv]} [/fo <Format>] [/nh]
whoami /all [/fo <Format>] [/nh]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/upn|ユーザー プリンシパル名 (UPN) 形式でユーザー名を表示します。|
|/fqdn|完全修飾ドメイン名 (FQDN) 形式でユーザー名を表示します。|
|/logonid|現在のユーザーのログオン ID が表示されます。|
|/user|現在のドメインとユーザー名およびセキュリティ識別子 (SID) が表示されます。|
|/groups|現在のユーザーが所属するユーザー グループが表示されます。|
|/priv|現在のユーザーのセキュリティ特権を表示します。|
|/fo\<形式 >|出力形式を指定します。 有効な値は次のとおりです。</br>**テーブル**テーブルの出力が表示されます。 これが既定値です。</br>**リスト**出力を一覧表示します。</br>**csv**コンマ区切り値 (CSV) 形式で出力を表示します。|
|/all|現在のユーザー名、セキュリティ識別子 (SID)、特権、および現在のユーザーが所属するグループを含め、現在のアクセス トークンでは、すべての情報を表示します。|
|/nh|列ヘッダーを出力に表示されないことを指定します。 これは、テーブルおよび CSV の形式に対してのみ有効です。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

現在このコンピューターにログオンしたユーザーのドメインとユーザー名を表示するには、次のように入力します。
```
whoami
```
次のような出力が表示されます。
```
DOMAIN1\administrator
```
現在のアクセス トークンでは、すべての情報を表示するに次のように入力します。
```
whoami /all
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)