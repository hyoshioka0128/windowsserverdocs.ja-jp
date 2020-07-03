---
title: nslookup set domain
description: Nslookup set domain コマンドの参照記事。既定のドメインネームシステム (DNS) のドメイン名を指定した名前に変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9d4d28e8-6e88-42cc-801f-94e9d8e051f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eaa12029beab301f955a4c9bed4595831f6ebf12
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934412"
---
# <a name="nslookup-set-domain"></a>nslookup set domain

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既定のドメインネームシステム (DNS) のドメイン名を指定した名前に変更します。

## <a name="syntax"></a>構文

```
set domain=<domainname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<domainname>` | 既定の DNS ドメイン名の新しい名前を指定します。 既定値はホストの名前です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 既定の DNS ドメイン名は、 **defname**と**検索**オプションの状態に応じて、参照要求に追加されます。

- DNS ドメインの検索一覧には、その名前に少なくとも2つのコンポーネントがある場合の既定の DNS ドメインの親が含まれます。 たとえば、既定の DNS ドメインが mfg.widgets.com の場合、検索リストには mfg.widgets.com と widgets.com の両方の名前が付けられます。

- [Nslookup set srchlist](nslookup-set-srchlist.md)コマンドを使用して別のリストを指定し、 [nslookup set all](nslookup-set-all.md)コマンドを使用して一覧を表示します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [nslookup set srchlist](nslookup-set-srchlist.md)

- [nslookup set all](nslookup-set-all.md)
