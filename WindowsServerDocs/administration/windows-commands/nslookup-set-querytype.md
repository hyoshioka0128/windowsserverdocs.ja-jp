---
title: nslookup set querytype
description: Nslookup set querytype コマンドのリファレンストピックでは、クエリのリソースレコードの種類を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c54671d23fb7fd9500ba7aac1d59cf50fef78ead
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721611"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クエリのリソースレコードの種類を変更します。 リソースレコードの種類の詳細については、「 [Request For Comment (Rfc) 1035](https://tools.ietf.org/html/rfc1035)」を参照してください。

> [!NOTE]
> このコマンドは、 [nslookup set type](nslookup-set-type.md)コマンドと同じです。

## <a name="syntax"></a>構文

```
set querytype=<resourcerecordtype>
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| `<resourcerecordtype>` | DNS リソースレコードの種類を指定します。 既定のリソースレコードの種類**はですが、次**のいずれかの値を使用できます。<ul><li>**A:** コンピューターの IP アドレスを指定します。</li><li>**任意:** コンピューターの IP アドレスを指定します。</li><li>**CNAME:** エイリアスの正規名を指定します。</li><li>**GID**グループ名のグループ識別子を指定します。</li><li>**HINFO:** コンピューターの CPU とオペレーティングシステムの種類を指定します。</li><li>**MB:** メールボックスドメイン名を指定します。</li><li>**MG:** メールグループメンバーを指定します。</li><li>**MINFO:** メールボックスまたはメールの一覧の情報を指定します。</li><li>**MR:** メールの名前変更ドメイン名を指定します。</li><li>**MX:** メールエクスチェンジャーを指定します。</li><li>**NS:** 名前付きゾーンの DNS ネームサーバーを指定します。</li><li>**PTR:** クエリが IP アドレスの場合は、コンピューター名を指定します。それ以外の場合は、他の情報へのポインターを指定します。</li><li>**SOA:** DNS ゾーンの権限の開始を指定します。</li><li>**TXT:** テキスト情報を指定します。</li><li>**UID:** ユーザー識別子を指定します。</li><li>**Uinfo:** ユーザー情報を指定します。</li><li>**WKS:** よく知られているサービスについて説明します。</li></ul> |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup set type](nslookup-set-type.md)
