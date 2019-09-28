---
title: ipxroute
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a30304f-655e-43d2-a4ac-7568abf8975c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd5f33766ff9b33c9d6020b7284f2fbf9552d44d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375334"
---
# <a name="ipxroute"></a>ipxroute

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

IPX プロトコルによって使用されるルーティングテーブルに関する情報を表示および変更します。 パラメーターを指定せずに使用します。 **ipxroute**には、不明、ブロードキャスト、およびマルチキャストアドレスに送信されるパケットの既定の設定が表示されます。   
## <a name="syntax"></a>構文  
```  
ipxroute servers [/type=X]  
ipxroute ripout <Network>  
ipxroute resolve {guid | name} {GUID | <AdapterName>}  
ipxroute board= N [def] [gbr] [mbr] [remove=xxxxxxxxxxxx]  
ipxroute config  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|サーバー [/type = X]|指定したサーバーの種類のサービスアクセスポイント (SAP) テーブルを表示します。  **X**は整数でなければなりません。 たとえば、 **/type = 4**の場合、すべてのファイルサーバーが表示されます。 **/Type**を指定しない場合、 **ipxroute servers**はすべての種類のサーバーを表示し、サーバー名で一覧表示します。|  
|ripout ネットワーク|IPX スタックのルートテーブルを調べ、必要に応じて rip 要求を送信することによって、*ネットワーク*に到達できるかどうかを検出します。  *Network*は、IPX ネットワークセグメント番号です。|  
|{guid&#124;名} {guid&#124;アダプター名} の解決|GUID の名前をフレンドリ名に解決するか、フレンドリ名をその GUID に解決します。|  
|ボード = *N*|パラメーターを照会または設定するネットワークアダプターを指定します。|  
|オート|パケットをすべてのルートブロードキャストに送信します。 パケットが送信元のルーティングテーブルにない一意のメディアアクセスカード (MAC) アドレスに送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。|  
|gbr|パケットをすべてのルートブロードキャストに送信します。 パケットがブロードキャストアドレス (FFFFFFFFFFFF) に送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。|  
|mbr|パケットをすべてのルートブロードキャストに送信します。 パケットがマルチキャストアドレス (C000xxxxxxxx) に送信された場合、 **ipxroute**は既定で1つのルートにパケットを送信します。|  
|削除 = *、*|指定されたノードアドレスをソースルーティングテーブルから削除します。|  
|構成|IPX が構成されているすべてのバインドに関する情報が表示されます。|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="BKMK_Examples"></a>例  
ワークステーションが接続されているネットワークセグメント、ワークステーションノードアドレス、および使用されているフレームの種類を表示するには、次のように入力します。  
```  
ipxroute config  
```  
## <a name="additional-references"></a>その他の参照情報  
-   [コマンド ライン構文の記号](command-line-syntax-key.md)  
