---
title: ipxroute
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a6d0cac3f835e86d40e03141c0da51d514ef0c6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724804"
---
# <a name="ipxroute"></a>ipxroute

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

IPX プロトコルによって使用されるルーティングテーブルに関する情報を表示および変更します。 パラメーターを指定せずに使用します。 **ipxroute**には、不明、ブロードキャスト、およびマルチキャストアドレスに送信されるパケットの既定の設定が表示されます。   
## <a name="syntax"></a>構文  
```  
ipxroute servers [/type=X]  
ipxroute ripout <Network>  
ipxroute resolve {guid | name} {GUID | <AdapterName>}  
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]  
ipxroute config  
```  
#### <a name="parameters"></a>パラメーター  
|パラメーター|[説明]|  
|-------|--------|  
|サーバー [/type = X]|指定したサーバーの種類のサービスアクセスポイント (SAP) テーブルを表示します。  **X**は整数でなければなりません。 たとえば、 **/type = 4**の場合、すべてのファイルサーバーが表示されます。 **/Type**を指定しない場合、 **ipxroute servers**はすべての種類のサーバーを表示し、サーバー名で一覧表示します。|  
|ripout ネットワーク|IPX スタックのルートテーブルを調べ、必要に応じて rip 要求を送信することによって、*ネットワーク*に到達できるかどうかを検出します。  *Network*は、IPX ネットワークセグメント番号です。|  
|{GUID&#124; name} {GUID&#124; AdapterName} を解決します|GUID の名前をフレンドリ名に解決するか、フレンドリ名をその GUID に解決します。|  
|ボード = *N*|パラメーターを照会または設定するネットワークアダプターを指定します。|  
|def|パケットをすべてのルートブロードキャストに送信します。 パケットが送信元のルーティングテーブルにない一意のメディアアクセスカード (MAC) アドレスに送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。|  
|gbr|パケットをすべてのルートブロードキャストに送信します。 パケットがブロードキャストアドレス (FFFFFFFFFFFF) に送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。|  
|mbr|パケットをすべてのルートブロードキャストに送信します。 パケットがマルチキャストアドレス (C000xxxxxxxx) に送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。|  
|削除 = *、*|指定されたノードアドレスをソースルーティングテーブルから削除します。|  
|config|IPX が構成されているすべてのバインドに関する情報が表示されます。|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="examples"></a>例  
ワークステーションが接続されているネットワークセグメント、ワークステーションノードアドレス、および使用されているフレームの種類を表示するには、次のように入力します。  
```  
ipxroute config  
```  
## <a name="additional-references"></a>その他のリファレンス  
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)  
