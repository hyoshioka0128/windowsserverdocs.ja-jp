---
title: tftp
description: リモート コンピューターからファイルを転送します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad195409076840fda0e8d6bf5cd0c295a62cdede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845903"
---
# <a name="tftp"></a>tftp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

通常、簡易のファイル転送プロトコル (tftp) サービスまたはデーモンを実行している UNIX を実行しているコンピューターのファイルと、リモート コンピューターの間を転送します。 tftp は通常、組み込みデバイスまたはファームウェア、または取得する構成については、システム イメージ、tftp サーバーからのブート プロセス中にシステムによって使用されます。   

## <a name="syntax"></a>構文  
```  
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]  
```  

### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|-i|バイナリ イメージの転送モード (オクテット モードとも呼ばれます) を指定します。 画像のバイナリ モードでファイルが 1 バイト単位で転送します。 バイナリ ファイルを転送するときに、このモードを使用します。 場合 **-i** は省略すると、ファイルが ASCII モードで転送します。 これは、既定の転送モードです。 このモードは、行の終わり (EOL) 文字を指定したコンピューターの適切な形式に変換します。 テキスト ファイルを転送するときに、このモードを使用します。 ファイル転送が成功した場合は、データ転送率が表示されます。|  
|\<ホスト\>|ローカルまたはリモート コンピューターを指定します。|  
|配置|ファイル転送 *ソース* ファイルをローカル コンピューターで *宛先* 、リモート コンピューター上です。 Tftp プロトコルがユーザー認証をサポートしていないため、ユーザーは、リモートのコンピューターにログオンする必要があり、ファイルは、リモート コンピューター上で書き込み可能である必要があります。|  
|get|ファイル転送 *宛先* ファイルへのリモート コンピューターで *ソース* 、ローカル コンピューター上です。|  
|\<ソース\>|転送するファイルを指定します。|  
|\<Destination (公開先)\>|ファイルを転送する場所を指定します。|  

## <a name="remarks"></a>注釈  
-   追加機能のウィザードを使用して tftp クライアントをインストールすることができます。  
-   Tftp プロトコルは任意の認証または暗号化メカニズムをサポートしていませんし、そのため、存在する場合は、セキュリティ上のリスクを導入することができます。 Tftp クライアントをインストールするには、インターネットに接続されているシステムには推奨されません。  
-   Tftp クライアント オプションのソフトウェアは、Windows Vista および Windows オペレーティング システムの以降のバージョンで非推奨としてマークします。 Microsoft は、tftp サーバー サービスはセキュリティ上の理由から備わっていません。  

## <a name="BKMK_Examples"></a>例  
ファイルをコピー **boot.img** リモート コンピューターから **Host1**します。  
```  
tftp  -i Host1 get boot.img  
```  

## <a name="additional-references"></a>その他の参照情報  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
