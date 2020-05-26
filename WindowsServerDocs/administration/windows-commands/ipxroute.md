---
title: ipxroute
description: Ipxroute コマンドのリファレンストピックでは、IPX プロトコルによって使用されるルーティングテーブルに関する情報を表示および変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afcb5064bc8d4eb4a3b4a8920fcfcf71591d7af5
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818322"
---
# <a name="ipxroute"></a>ipxroute

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

IPX プロトコルによって使用されるルーティングテーブルに関する情報を表示および変更します。 パラメーターを指定せずに使用します。 **ipxroute**には、不明、ブロードキャスト、およびマルチキャストアドレスに送信されるパケットの既定の設定が表示されます。

## <a name="syntax"></a>構文

```
ipxroute servers [/type=x]
ipxroute ripout <network>
ipxroute resolve {guid | name} {GUID | <adaptername>}
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]
ipxroute config
```

### <a name="parameters"></a>パラメーター
| パラメーター | 説明 |
| ------- | -------- |
| サーバー`[/type=x]` | 指定したサーバーの種類のサービスアクセスポイント (SAP) テーブルを表示します。 **x**は整数でなければなりません。 たとえば、は `/type=4` すべてのファイルサーバーを表示します。 [ **/Type**] を指定しない場合は、 `ipxroute servers` すべての種類のサーバーが表示され、サーバー名で一覧表示されます。 |
| 解決 `{GUID | name}``{GUID | adaptername}` | GUID の名前をフレンドリ名に解決するか、フレンドリ名をその GUID に解決します。 |
| ボード = *n* | パラメーターを照会または設定するネットワークアダプターを指定します。 |
| def | パケットをすべてのルートブロードキャストに送信します。 パケットが送信元のルーティングテーブルにない一意のメディアアクセスカード (MAC) アドレスに送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。 |
| gbr | パケットをすべてのルートブロードキャストに送信します。 パケットがブロードキャストアドレス (FFFFFFFFFFFF) に送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。 |
| mbr | パケットをすべてのルートブロードキャストに送信します。 パケットがマルチキャストアドレス (C000xxxxxxxx) に送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。 |
| 削除 =*、* | 指定されたノードアドレスをソースルーティングテーブルから削除します。 |
| config | IPX が構成されているすべてのバインドに関する情報が表示されます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

ワークステーションが接続されているネットワークセグメント、ワークステーションノードアドレス、および使用されているフレームの種類を表示するには、次のように入力します。

```
ipxroute config
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
