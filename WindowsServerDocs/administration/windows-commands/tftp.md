---
title: tftp
description: リモートコンピューターとの間でファイルを転送します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b3674cbfdbc01811ece57e2f9cbbea3aa31251d
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84223044"
---
# <a name="tftp"></a>tftp

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

は、簡易ファイル転送プロトコル (tftp) サービスまたはデーモンを実行しているリモートコンピューター (通常は UNIX を実行しているコンピューター) との間でファイルを転送します。 tftp は通常、tftp サーバーからのブートプロセス中にファームウェア、構成情報、またはシステムイメージを取得する組み込みデバイスまたはシステムによって使用されます。

## <a name="syntax"></a>構文
```
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]
```

#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-i|バイナリ イメージの転送モード (オクテット モードとも呼ばれます) を指定します。 画像のバイナリ モードでファイルが 1 バイト単位で転送します。 バイナリ ファイルを転送するときに、このモードを使用します。 場合 **-i** は省略すると、ファイルが ASCII モードで転送します。 これは、既定の転送モードです。 このモードは、行の終わり (EOL) 文字を指定したコンピューターの適切な形式に変換します。 テキスト ファイルを転送するときに、このモードを使用します。 ファイル転送が成功した場合は、データ転送率が表示されます。|
|\<Host\>|ローカルまたはリモート コンピューターを指定します。|
|put|ファイル転送 *ソース* ファイルをローカル コンピューターで *宛先* 、リモート コンピューター上です。 Tftp プロトコルではユーザー認証がサポートされていないため、ユーザーはリモートコンピューターにログオンする必要があり、ファイルはリモートコンピューター上で書き込み可能である必要があります。|
|get|ファイル転送 *宛先* ファイルへのリモート コンピューターで *ソース* 、ローカル コンピューター上です。|
|\<Source\>|転送するファイルを指定します。|
|\<Destination\>|ファイルを転送する場所を指定します。|

## <a name="remarks"></a>解説
-   Tftp クライアントは、機能の追加ウィザードを使用してインストールできます。
-   Tftp プロトコルでは、認証または暗号化のメカニズムはサポートされていないため、セキュリティ上のリスクが生じる可能性があります。 インターネットに接続されているシステムには、tftp クライアントをインストールすることはお勧めしません。
-   Tftp クライアントはオプションのソフトウェアで、Windows Vista 以降のバージョンの Windows オペレーティングシステムでは非推奨としてマークされています。 Tftp サーバーサービスは、セキュリティ上の理由からマイクロソフトによって提供されなくなりました。

## <a name="examples"></a>例
ファイルをコピー **boot.img** リモート コンピューターから **Host1**します。
```
tftp  -i Host1 get boot.img
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)
