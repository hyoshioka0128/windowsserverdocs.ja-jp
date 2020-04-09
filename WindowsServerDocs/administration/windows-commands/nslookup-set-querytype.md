---
title: nslookup set querytype
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c066277a22325e5db8383f58cda31038aa656e0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838435"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリのリソースレコードの種類を変更します。
## <a name="syntax"></a>構文
```
set querytype=<ResourceRecordtype>
```
### <a name="parameters"></a>パラメーター
<ResourceRecordtype> DNS リソースレコードの種類を指定します。 既定のリソースレコードの種類はです。次の表に、このコマンドの有効な値を示します。

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
|  NS   |                                 名前付きゾーンの DNS ネームサーバーを指定します。                                 |
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
  < href = key.md =-コマンドライン構文の[キー](command-line-syntax-key.md)> コマンドライン構文のキー</a> < href = nslookup-set-type.md data-raw-source =[nslookup set type](nslookup-set-type.md)> nslookup set type」のように入力してください</a>
