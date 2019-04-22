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
ms.openlocfilehash: 5d698e6d4603afb332efeaf1cdc79eeeee37d66d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813123"
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
|Value|説明|
|-----|--------|
|A|コンピューターの IP アドレスを指定します|
|任意|コンピューターの IP アドレスを指定します。|
|CNAME|エイリアスの正規名を指定します。|
|GID|グループ名のグループ識別子を指定します。|
|HINFO|コンピューターの CPU およびオペレーティング システムの種類を指定します。|
|MB|メールボックスのドメイン名を指定します。|
|MG|メール グループのメンバーを指定します。|
|MINFO|メールボックスまたはメール リスト情報を指定します。|
|MR|メールの名前の変更のドメイン名を指定します。|
|MX|メール エクスチェン ジャーを指定します。|
|NS|名前付きのゾーンの DNS ネーム サーバーを指定します。|
|PTR|コンピューターを指定する場合は、クエリは、IP アドレスの名前それ以外の場合、その他の情報へのポインターを指定します。|
|SOA|DNS ゾーンの権限の開始-を指定します。|
|TXT|テキスト情報を指定します。|
|UID|ユーザー識別子を指定します。|
|UINFO|ユーザー情報を指定します。|
|WKS|よく知られているサービスをについて説明します。|
{0} のヘルプ | ?}
簡単な概要を表示します**nslookup**サブコマンド。
## <a name="remarks"></a>注釈
-   **セットの種類**コマンドと同じ機能を実行する、 **querytype 設定**コマンド。
-   リソース レコードの種類の詳細については、Request for Comment (Rfc) 1035 を参照してください。
## <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[nslookup の種類を設定します。](nslookup-set-type.md)
