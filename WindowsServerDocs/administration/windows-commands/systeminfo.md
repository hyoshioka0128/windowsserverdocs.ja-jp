---
title: systeminfo
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 32a84a33c5339e9949648a4e40d71daf25c055d8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370692"
---
# <a name="systeminfo"></a>systeminfo



コンピューターとオペレーティング システムの構成、セキュリティ情報、製品 ID、および (RAM、ディスク領域のネットワーク カードなど) のハードウェア プロパティを含む、オペレーティング システムの構成情報の詳細表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s \<Computer >|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u \<Domain > \< Username >|指定したユーザー アカウントのアカウント権限でコマンドを実行します。 場合 **/u** が指定されていない、このコマンドは、現在のコマンドを発行しているコンピューターにログオンしたユーザーのアクセス許可を使用します。|
|/p \<パスワード >|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/fo \<Format >|次の値のいずれかで出力形式を指定します。</br>一覧テーブルに出力を表示します。</br>表出力を一覧に表示します。</br>市区出力をコンマ区切り値形式で表示します。|
|/nh|出力に列ヘッダーを抑制します。 有効な場合に、 **/fo** パラメーターがテーブルまたは CSV に設定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

Srvmain という名前のコンピューターの構成情報を表示するには、次のように入力します。

**systeminfo/s srvmain**

Maindom ドメインに配置されている Srvmain2 という名前のコンピューターの構成情報をリモートで表示するには、次のように入力します。

**systeminfo/s srvmain2/u maindom\hiropln**

Maindom ドメインに配置されている Srvmain2 という名前のコンピューターの構成情報を (一覧形式で) リモートで表示するには、次のように入力します。

**systeminfo/s srvmain2/u maindom\hiropln/p p@ssW23/fo list**

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)