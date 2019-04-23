---
title: ftp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 758335e1-fd8d-448c-a654-993126239dd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76b8a2ee7ce81a6db75e0d375d017746e4361df1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887383"
---
# <a name="ftp"></a>ftp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送プロトコル (ftp) サーバー サービスを実行しているコンピューターからファイルを転送します。 **ftp** ASCII テキスト ファイルを処理して対話的にまたはバッチ モードで使用できます。 
## <a name="syntax"></a>構文
```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<FileName>] [-a] [-A] [-x:<SendBuffer>] [-r:<RecvBuffer>] [-b:<AsyncBuffers>][-w:<WindowsSize>]  [-?] [<Host>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-v|リモート サーバーの応答を表示をしません。|
|-d|デバッグ、FTP クライアントと FTP サーバーの間で渡されるすべてのコマンドを表示できるようにします。|
|-i|複数のファイル転送中に対話型プロンプトを無効にします。|
|-n|初期接続時に自動ログインを抑制します。|
|-g|ファイル名グロビングを無効にします。  **Glob** ローカル ファイルとパス名にワイルドカード文字としてアスタリスク (*) と疑問符 (?) の使用を許可します。 詳細については、次を参照してください。[その他の参照](ftp.md#BKMK_additionalRef)します。|
|-%s: です。<FileName>|含むテキスト ファイルを指定 **ftp** コマンドです。 これらのコマンドを実行した後に自動的に **ftp** を開始します。 このパラメーターには、スペースは許可されません。 リダイレクトではなく、このパラメーターを使用して (**<**)。 **注:** Windows 8 および Windows Server 2012 またはそれ以降のオペレーティング システムでは、utf-8 でテキスト ファイルを記述する必要があります。|
|-a|Ftp データ接続をバインドするときに、任意のローカル インターフェイスを使用できることを指定します。|
|A|匿名として ftp サーバーにログオンします。|
|-x:<SendBuffer>|8192 の既定の SO_SNDBUF サイズをオーバーライドします。|
|-r:<RecvBuffer>|8192 の既定の SO_RCVBUF サイズをオーバーライドします。|
|-b:<AsyncBuffers>|3 の既定の非同期バッファー数を上書きします。|
|-w: です。<WindowsSize>|転送バッファーのサイズを指定します。 既定のウィンドウ サイズは、4096 バイトです。|
|-?|コマンド プロンプトにヘルプを表示します。|
|<host>|コンピューター名、IP アドレス、または接続先の ftp サーバーの IPv6 アドレスを指定します。 ホスト名またはアドレスを指定した場合は、行の最後のパラメーターになる可能性があります。|
## <a name="remarks"></a>注釈
-   詳細については**ftp** Windows Server 2003 でのコマンドを参照してください[ftp](https://technet.microsoft.com/library/cc756013(v=ws.10).aspx)します。
-   **ftp**コマンド ライン パラメーターは大文字小文字を区別します。
-   このコマンドは、使用可能な場合にのみ、 **インターネット プロトコル (TCP/IP)** プロトコルはネットワーク接続のネットワーク アダプターのプロパティ内のコンポーネントとしてインストールします。
-   **ftp**対話的に使用できます。 起動すると、 **ftp** により、使用することができますサブ環境 **ftp** コマンドです。 」と入力して、コマンド プロンプトに返すことができます、 **終了** コマンドです。 ときに、 **ftp** サブ環境が実行されている場合で示された、 **ftp >** コマンド プロンプト。 詳細については、次を参照してください。、 **ftp** コマンドです。
-   **ftp** IPv6 プロトコルがインストールされている場合は、IPv6 の使用をサポートしています。 詳細については、次を参照してください。[その他の参照](ftp.md#BKMK_additionalRef)します。
## <a name="BKMK_Examples"></a>例
Ftp.example.microsoft.com をという名前の ftp サーバーにログオンするのには、次のように入力します。
```
ftp ftp.example.microsoft.com
```
名前付き ftp.example.microsoft.com および実行する ftp サーバーにログオンする、 **ftp** resync.txt、型をという名前のファイルに含まれるコマンド。
```
ftp -s:resync.txt ftp.example.microsoft.com
```
## <a name="BKMK_additionalRef"></a>その他の参照
-   [IP バージョン 6](https://technet.microsoft.com/library/cc738636(v=ws.10).aspx)
-   [IPv6 アプリケーション](https://technet.microsoft.com/library/cc782509(v=ws.10).aspx)
-   [コマンドライン構文キー](command-line-syntax-key.md)
