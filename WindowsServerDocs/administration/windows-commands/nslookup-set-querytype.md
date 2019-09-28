---
title: nslookup set querytype
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc0eb19fd66e738b4bfc110a2bbc172153a12d98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372904"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリのリソースレコードの種類を変更します。
## <a name="syntax"></a>構文
```
set querytype=<ResourceRecordtype>
```
## <a name="parameters"></a>パラメーター
<ResourceRecordtype>DNS リソースレコードの種類を指定します。 既定のリソースレコードの種類はです。次の表に、このコマンドの有効な値を示します。

| 値 |                                                   説明                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   A   |                                      コンピューター&#39;の IP アドレスを指定します                                      |
|  いつ  |                                     コンピューター&#39;の IP アドレスを指定します。                                      |
| CNAME |                                    エイリアスの正規名を指定します。                                     |
|  ―  |                                  グループ名のグループ識別子を指定します。                                  |
| HINFO |                          コンピューター&#39;の CPU とオペレーティングシステムの種類を指定します。                           |
|  MB   |                                        メールボックスドメイン名を指定します。                                         |
|  MG   |                                         メールグループメンバーを指定します。                                          |
| MINFO |                                   メールボックスまたはメールの一覧の情報を指定します。                                   |
|  MR   |                                     メールの名前変更ドメイン名を指定します。                                      |
|  MX   |                                          メールエクスチェンジャーを指定します。                                          |
|  STATION   |                                 名前付きゾーンの DNS ネームサーバーを指定します。                                 |
|  ポインター  | クエリが IP アドレスの場合は、コンピューター名を指定します。それ以外の場合は、他の情報へのポインターを指定します。 |
|  SOA  |                                DNS ゾーンの権限の開始を指定します。                                 |
|  TXT  |                                         テキスト情報を指定します。                                         |
|  UID  |                                         ユーザー識別子を指定します。                                          |
| UINFO |                                         ユーザー情報を指定します。                                         |
|  WKS  |                                         よく知られているサービスについて説明します。                                         |
| {ヘルプ |                                                       ?}                                                        |

<strong>Nslookup</strong>サブコマンドの簡単な概要を表示します。
## <a name="remarks"></a>コメント
- <strong>Set type</strong>コマンドは、 <strong>set querytype</strong>コマンドと同じ機能を実行します。
- リソースレコードの種類の詳細については、「Request for Comment (Rfc) 1035」を参照してください。
  ## <a name="additional-references"></a>その他の参照情報
  <a href="command-line-syntax-key.md" data-raw-source="[Command-Line Syntax Key](command-line-syntax-key.md)">コマンドライン構文のキー</a>
  <a href="nslookup-set-type.md" data-raw-source="[nslookup set type](nslookup-set-type.md)">nslookup set type</a>
