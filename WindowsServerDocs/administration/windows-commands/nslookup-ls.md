---
title: nslookup ls
description: Nslookup ls コマンドのリファレンストピック。 DNS ドメイン情報が一覧表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87e30ed5d5b44b805c3b3b004feb5ed252b5a760
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721125"
---
# <a name="nslookup-ls"></a>nslookup ls

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

DNS ドメイン情報を一覧表示します。

## <a name="syntax"></a>構文

```
ls [<option>] <DNSdomain> [{[>] <filename>|[>>] <filename>}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| `<option>` | 有効なオプションは次のとおりです。<ul><li>**-t:** 指定された種類のすべてのレコードを一覧表示します。 詳細については、「 [nslookup set querytype](nslookup-set-querytype.md)」を参照してください。</li><li>**-a:** DNS ドメイン内のコンピューターのエイリアスを一覧表示します。 このパラメーターは、 **-t CNAME**と同じです。</li><li>**-d:** DNS ドメインのすべてのレコードを一覧表示します。 このパラメーターは、 **-t ANY**と同じです。</li><li>**-h:** DNS ドメインの CPU とオペレーティングシステムの情報を一覧表示します。 このパラメーターは、 **-t HINFO**と同じです。</li><li>**-s:** DNS ドメイン内のコンピューターのよく知られているサービスを一覧表示します。 このパラメーターは、 **-t WKS**と同じです。 |
| `<DNSdomain>` | 情報を必要とする DNS ドメインを指定します。 |
| `<filename>` | 保存された出力に使用するファイル名を指定します。 より大きい ( `>` ) 文字と2つ以上の文字 () を使用して、 `>>` 通常の方法で出力をリダイレクトできます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- このコマンドの既定の出力には、コンピューター名とそれに関連付けられた IP アドレスが含まれます。

- 出力がファイルに送られた場合、サーバーから受信した50レコードごとにハッシュマークが追加されます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup set querytype](nslookup-set-querytype.md)
