---
title: nslookup set querytype
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f0015db716bd8c74bc4366063009bda41d338d19
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436729"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリのリソース レコードの種類を変更します。
## <a name="syntax"></a>構文
```
set querytype=<ResourceRecordtype>
```
## <a name="parameters"></a>パラメーター
<ResourceRecordtype> DNS リソース レコードの種類を指定します。 既定のリソース レコードの種類は A です。次の表では、このコマンドの有効な値を示します。

| Value |                                                   説明                                                   |
|-------|-----------------------------------------------------------------------------------------------------------------|
|   A   |                                      コンピューターを指定します&#39;の IP アドレス                                      |
|  任意  |                                     コンピューターを指定します&#39;の IP アドレス。                                      |
| CNAME |                                    エイリアスの正規名を指定します。                                     |
|  GID  |                                  グループ名のグループ識別子を指定します。                                  |
| HINFO |                          コンピューターを指定します&#39;s CPU およびオペレーティング システムの種類。                           |
|  MB   |                                        メールボックスのドメイン名を指定します。                                         |
|  MG   |                                         メール グループのメンバーを指定します。                                          |
| MINFO |                                   メールボックスまたはメール リスト情報を指定します。                                   |
|  MR   |                                     メールの名前の変更のドメイン名を指定します。                                      |
|  MX   |                                          メール エクスチェン ジャーを指定します。                                          |
|  NS   |                                 名前付きのゾーンの DNS ネーム サーバーを指定します。                                 |
|  PTR  | コンピューターを指定する場合は、クエリは、IP アドレスの名前それ以外の場合、その他の情報へのポインターを指定します。 |
|  SOA  |                                DNS ゾーンの権限の開始-を指定します。                                 |
|  TXT  |                                         テキスト情報を指定します。                                         |
|  UID  |                                         ユーザー識別子を指定します。                                          |
| UINFO |                                         ユーザー情報を指定します。                                         |
|  WKS  |                                         よく知られているサービスをについて説明します。                                         |
| {0} のヘルプ |                                                       ?}                                                        |

簡単な概要を表示します<strong>nslookup</strong>サブコマンド。
## <a name="remarks"></a>注釈
- <strong>セットの種類</strong>コマンドと同じ機能を実行する、 <strong>querytype 設定</strong>コマンド。
- リソース レコードの種類の詳細については、Request for Comment (Rfc) 1035 を参照してください。
  ## <a name="additional-references"></a>その他の参照
  <a href="command-line-syntax-key.md" data-raw-source="[Command-Line Syntax Key](command-line-syntax-key.md)">コマンドライン構文のポイント</a>
  <a href="nslookup-set-type.md" data-raw-source="[nslookup set type](nslookup-set-type.md)">nslookup の種類を設定します。</a>
