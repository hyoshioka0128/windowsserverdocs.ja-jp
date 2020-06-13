---
title: nslookup set
description: Nslookup set コマンドのリファレンストピック。参照の動作に影響する構成設定を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1fe5b36d-e93e-468b-abca-43b0204b32d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 579334b3b6b0cd5e9373876144f46fa21d57c745
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721185"
---
# <a name="nslookup-set"></a>nslookup set

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

参照の機能に影響する構成設定を変更します。

## <a name="syntax"></a>構文

```
set all [class | d2 | debug | domain | port | querytype | recurse | retry | root | search | srchlist | timeout | type | vc] [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| [nslookup set all](nslookup-set-all.md) | 現在のすべての設定を一覧表示します。 |
| [nslookup set class](nslookup-set-class.md) | 情報のプロトコルグループを指定するクエリクラスを変更します。 |
| [nslookup set d2](nslookup-set-d2.md) | 詳細デバッグモードをオンまたはオフにします。 |
| [nslookup set debug](nslookup-set-debug.md) | デバッグモードを完全にオフにします。 |
| [nslookup set domain](nslookup-set-domain.md) | 既定のドメインネームシステム (DNS) のドメイン名を指定した名前に変更します。 |
| [nslookup set port](nslookup-set-port.md) | 既定の TCP/UDP ドメインネームシステム (DNS) ネームサーバーポートを、指定された値に変更します。
| [nslookup set querytype](nslookup-set-querytype.md) | クエリのリソースレコードの種類を変更します。 |
| [nslookup set recurse](nslookup-set-recurse.md) | 他のサーバーに対して情報が見つからない場合にクエリを実行するように、ドメインネームシステム (DNS) ネームサーバーに指示します。 |
| [nslookup set retry](nslookup-set-retry.md) | 再試行回数を設定します。 |
| [nslookup set root](nslookup-set-root.md) | クエリに使用するルートサーバーの名前を変更します。 |
| [nslookup set search](nslookup-set-search.md) | DNS ドメイン検索リスト内のドメインネームシステム (DNS) ドメイン名を、応答が受信されるまで要求に追加します。 |
| [nslookup set srchlist](nslookup-set-srchlist.md) | 既定のドメインネームシステム (DNS) のドメイン名と検索一覧を変更します。 |
| [nslookup set timeout](nslookup-set-timeout.md) | 検索要求への応答を待機する秒数の初期値を変更します。 |
| [nslookup set type](nslookup-set-type.md) | クエリのリソースレコードの種類を変更します。 |
| [nslookup set vc](nslookup-set-vc.md) | サーバーに要求を送信するときに仮想回線を使用するかどうかを指定します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
