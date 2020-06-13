---
title: nslookup set search
description: Nslookup set search コマンドのリファレンストピック。応答が受信されるまで、DNS ドメインの検索リストにドメインネームシステム (DNS) のドメイン名を要求に追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3219434f768a573c9e433c44b6b38bc9dc75f14
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721427"
---
# <a name="nslookup-set-search"></a>nslookup set search

DNS ドメイン検索リスト内のドメインネームシステム (DNS) ドメイン名を、応答が受信されるまで要求に追加します。 これは、セットと参照要求に少なくとも1つのピリオドが含まれている場合に適用されますが、末尾にピリオドは付きません。

## <a name="syntax"></a>構文

```
set [no]search
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| nosearch | 要求の DNS ドメイン検索一覧にドメインネームシステム (DNS) ドメイン名の追加を停止します。 |
| search | 応答が受信されるまで、要求の DNS ドメイン検索一覧にドメインネームシステム (DNS) のドメイン名を追加します。 これが既定値です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
