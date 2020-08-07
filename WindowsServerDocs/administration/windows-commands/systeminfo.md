---
title: systeminfo
description: Systeminfo の参照記事。オペレーティングシステムの構成、セキュリティ情報、製品 ID、ハードウェアのプロパティ (RAM、ディスク領域、ネットワークカードなど) を含む、コンピューターとそのオペレーティングシステムに関する詳細な構成情報が表示されます。
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b34e92a5035360cb600bfe73b405f0a7033b6196
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881905"
---
# <a name="systeminfo"></a>systeminfo

コンピューターとオペレーティング システムの構成、セキュリティ情報、製品 ID、および (RAM、ディスク領域のネットワーク カードなど) のハードウェア プロパティを含む、オペレーティング システムの構成情報の詳細表示します。



## <a name="syntax"></a>構文

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<Computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定値はローカル コンピューターです。|
|/u\<Domain>\<UserName>|指定したユーザー アカウントのアカウント権限でコマンドを実行します。 場合 **/u** が指定されていない、このコマンドは、現在のコマンドを発行しているコンピューターにログオンしたユーザーのアクセス許可を使用します。|
|/p\<Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/fo\<Format>|次の値のいずれかで出力形式を指定します。</br>テーブル: テーブルの出力を表示します。</br>:] ボックスの一覧は、リスト内の出力を表示します。</br>CSV: は、コンマ区切り値形式で出力を表示します。|
|/nh|出力に列ヘッダーを抑制します。 有効な場合に、 **/fo** パラメーターがテーブルまたは CSV に設定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="examples"></a>例

Srvmain という名前のコンピューターの構成情報を表示するには、次のように入力します。

**systeminfo/s srvmain**

Maindom ドメインに配置されている Srvmain2 という名前のコンピューターの構成情報をリモートで表示するには、次のように入力します。

**systeminfo/s srvmain2/u maindom\hiropln**

Maindom ドメインに配置されている Srvmain2 という名前のコンピューターの構成情報を (一覧形式で) リモートで表示するには、次のように入力します。

**systeminfo/s srvmain2/u maindom\hiropln/p p@ssW23 /fo list**

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)