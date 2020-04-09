---
title: systeminfo
description: Systeminfo の Windows コマンドのトピック。オペレーティングシステムの構成、セキュリティ情報、製品 ID、ハードウェアのプロパティ (RAM、ディスク領域、ネットワークカードなど) を含む、コンピューターとそのオペレーティングシステムに関する詳細な構成情報が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41c2a499bc10f5b44f250958471b90f4b88dfede
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833575"
---
# <a name="systeminfo"></a>systeminfo

コンピューターとオペレーティング システムの構成、セキュリティ情報、製品 ID、および (RAM、ディスク領域のネットワーク カードなど) のハードウェア プロパティを含む、オペレーティング システムの構成情報の詳細表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s \<コンピューター >|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u \<ドメイン >\<ユーザー名 >|指定したユーザー アカウントのアカウント権限でコマンドを実行します。 場合 **/u** が指定されていない、このコマンドは、現在のコマンドを発行しているコンピューターにログオンしたユーザーのアクセス許可を使用します。|
|/p \<パスワード >|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/fo \<形式 >|次の値のいずれかで出力形式を指定します。</br>テーブル: テーブルの出力を表示します。</br>: ボックスの一覧は、リスト内の出力を表示します。</br>CSV: は、コンマ区切り値形式で出力を表示します。|
|/nh|出力に列ヘッダーを抑制します。 有効な場合に、 **/fo** パラメーターがテーブルまたは CSV に設定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

Srvmain という名前のコンピューターの構成情報を表示するには、次のように入力します。

**systeminfo/s srvmain**

Maindom ドメインに配置されている Srvmain2 という名前のコンピューターの構成情報をリモートで表示するには、次のように入力します。

**systeminfo/s srvmain2/u maindom\hiropln**

Maindom ドメインに配置されている Srvmain2 という名前のコンピューターの構成情報を (一覧形式で) リモートで表示するには、次のように入力します。

**systeminfo/s srvmain2/u maindom\hiropln/p p@ssW23/fo list**

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)