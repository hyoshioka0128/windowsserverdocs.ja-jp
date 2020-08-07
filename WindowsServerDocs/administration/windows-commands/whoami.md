---
title: whoami
description: ローカルシステムに現在ログオンしているユーザーのユーザー、グループ、特権に関する情報を表示する、whoami の参照記事です。
ms.topic: article
ms.assetid: 6e3f4d5c-f1f5-4429-b602-afad2b3488bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdcef4072fe692f2717fe79814af926a2c151636
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896494"
---
# <a name="whoami"></a>whoami



ローカルシステムに現在ログオンしているユーザーのユーザー、グループ、および特権に関する情報を表示します。 パラメーターを指定せずに使用する場合、 **whoami** 、現在のドメインとユーザー名を表示します。



## <a name="syntax"></a>構文

```
whoami [/upn | /fqdn | /logonid]
whoami {[/user] [/groups] [/priv]} [/fo <Format>] [/nh]
whoami /all [/fo <Format>] [/nh]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/upn|ユーザー名をユーザープリンシパル名 (UPN) 形式で表示します。|
|/fqdn|完全修飾ドメイン名 (FQDN) 形式でユーザー名を表示します。|
|/logonid|現在のユーザーのログオン ID を表示します。|
|/user|現在のドメインとユーザー名、およびセキュリティ識別子 (SID) が表示されます。|
|/groups|現在のユーザーが所属するユーザーグループを表示します。|
|/priv|現在のユーザーのセキュリティ特権を表示します。|
|/fo\<Format>|出力形式を指定します。 有効な値は、次のとおりです。</br>**テーブル**テーブルに出力を表示します。 これが既定値です。</br>**リスト**出力を一覧に表示します。</br>**csv**出力をコンマ区切り値 (CSV) 形式で表示します。|
|/all|現在のユーザー名、セキュリティ識別子 (SID)、特権、および現在のユーザーが属するグループを含む、現在のアクセストークンのすべての情報を表示します。|
|/nh|列ヘッダーを出力に表示しないことを指定します。 これは、テーブル形式と CSV 形式に対してのみ有効です。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="examples"></a>例

現在このコンピューターにログオンしているユーザーのドメインとユーザー名を表示するには、次のように入力します。
```
whoami
```
次のような出力が表示されます。
```
DOMAIN1\administrator
```
現在のアクセストークンのすべての情報を表示するには、次のように入力します。
```
whoami /all
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)