---
title: ipxroute
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d995204eea0af776a2084a82411fa95542d1d77a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889093"
---
# <a name="ipxroute"></a>ipxroute

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

表示され、IPX プロトコルで使用されるルーティング テーブルに関する情報を変更します。 パラメーターを指定せずに使用される**ipxroute**不明な、ブロードキャストおよびマルチキャスト アドレスに送信されるパケットの既定の設定を表示します。   
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
|servers[ /type=X]|指定したサーバーの種類のサービスへのアクセス ポイント (SAP) テーブルが表示されます。  **X**整数を指定する必要があります。 たとえば、 **/type 4 =** すべてのファイル サーバーが表示されます。 指定しない場合 **/type**、 **ipxroute サーバー**サーバー名で一覧表示するサーバーのすべての種類が表示されます。|  
|ripout ネットワーク|場合を検出します*ネットワーク*に到達可能で、IPX stack のルート テーブルのコンサルティングおよび必要に応じて、rip の要求を送信します。  *ネットワーク*IPX ネットワーク セグメントの数です。|  
|解決するには {GUID&#124;名} {GUID&#124; AdapterName}|GUID の名前をそのフレンドリ名、またはその GUID にフレンドリ名を解決します。|  
|ボード = *N*|クエリまたはパラメーターを設定する対象のネットワーク アダプターを指定します。|  
|def|すべてのルートをブロードキャストするパケットを送信します。 ソースのルーティング テーブルではない一意のメディア アクセス制御 (MAC) アドレス、パケットが転送される場合**ipxroute**既定ではブロードキャストの 1 つのルートにパケットを送信します。|  
|gbr|すべてのルートをブロードキャストするパケットを送信します。 ブロードキャスト アドレス (FFFFFFFFFFFF) にパケットを転送する場合**ipxroute**既定ではブロードキャストの 1 つのルートにパケットを送信します。|  
|mbr|すべてのルートをブロードキャストするパケットを送信します。 マルチキャスト アドレス (C000xxxxxxxx)、パケットが転送される場合**ipxroute**既定ではブロードキャストの 1 つのルートにパケットを送信します。|  
|remove= *xxxxxxxxxxxx*|ソースのルーティング テーブルから特定のノードのアドレスを削除します。|  
|構成|すべての IPX が構成されているバインドに関する情報が表示されます。|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="BKMK_Examples"></a>例  
ワークステーションがアタッチされているネットワーク セグメントでは、ワークステーション ノードのアドレス、および使用されているフレームの種類を表示するには、次のように入力します。  
```  
ipxroute config  
```  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
