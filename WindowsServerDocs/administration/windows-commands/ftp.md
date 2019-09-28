---
title: ftp
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b64e6831fcf8930c62b2a3f04022dc49d5297683
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375859"
---
# <a name="ftp"></a>ftp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送プロトコル (ftp) サーバーサービスを実行しているコンピューターとの間でファイルを転送します。 **ftp**は、ASCII テキストファイルを処理することによって、対話形式またはバッチモードで使用できます。 
## <a name="syntax"></a>構文
```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<FileName>] [-a] [-A] [-x:<SendBuffer>] [-r:<RecvBuffer>] [-b:<AsyncBuffers>][-w:<WindowsSize>]  [-?] [<Host>]
```
### <a name="parameters"></a>パラメーター

|     パラメーター     |                                                                                                                                                      説明                                                                                                                                                      |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        -v         |                                                                                                                                    リモート サーバーの応答を表示をしません。                                                                                                                                     |
|        -d         |                                                                                                               デバッグを有効にし、FTP クライアントと FTP サーバーの間で渡されたすべてのコマンドを表示します。                                                                                                                |
|        -i         |                                                                                                                            複数のファイル転送中の対話形式のプロンプトを無効にします。                                                                                                                             |
|        -n         |                                                                                                                                    初期接続時に自動ログインを抑制します。                                                                                                                                     |
|        -g         |                                         ファイル名グロビングを無効にします。  **[Glob]** を使用すると、ローカルファイルとパス名にアスタリスク (\*) と疑問符 (?) をワイルドカード文字として使用できます。 詳細については、「[その他の参照](ftp.md#BKMK_additionalRef)情報」を参照してください。                                          |
|   -s: <FileName>   | 含むテキスト ファイルを指定 **ftp** コマンドです。 これらのコマンドを実行した後に自動的に **ftp** を開始します。 このパラメーターには、スペースは許可されません。 リダイレクトではなく、このパラメーターを使用して ( **<** )。 **注:** Windows 8 および Windows Server 2012 以降のオペレーティングシステムでは、テキストファイルを UTF-8 で記述する必要があります。 |
|        -a         |                                                                                                                 Ftp データ接続をバインドするときに、任意のローカルインターフェイスを使用できることを指定します。                                                                                                                  |
|        A         |                                                                                                                                        Ftp サーバーに匿名でログオンします。                                                                                                                                         |
|  -x: <SendBuffer>  |                                                                                                                                     8192 の既定の SO_SNDBUF サイズをオーバーライドします。                                                                                                                                     |
|  -r: <RecvBuffer>  |                                                                                                                                     8192 の既定の SO_RCVBUF サイズをオーバーライドします。                                                                                                                                     |
| -b: <AsyncBuffers> |                                                                                                                                    3 の既定の非同期バッファー数を上書きします。                                                                                                                                     |
| -w: <WindowsSize>  |                                                                                                                   転送バッファーのサイズを指定します。 既定のウィンドウ サイズは、4096 バイトです。                                                                                                                   |
|        -?         |                                                                                                                                         コマンド プロンプトにヘルプを表示します。                                                                                                                                          |
|      <host>       |                                                                    接続先の ftp サーバーのコンピューター名、IP アドレス、または IPv6 アドレスを指定します。 ホスト名またはアドレスを指定した場合は、行の最後のパラメーターになる可能性があります。                                                                    |

## <a name="remarks"></a>コメント
- Windows Server 2003 の**ftp**コマンドの詳細については、「 [ftp](https://technet.microsoft.com/library/cc756013(v=ws.10).aspx)」を参照してください。
- **ftp**コマンドラインパラメーターでは、大文字と小文字が区別されます。
- このコマンドは、使用可能な場合にのみ、 **インターネット プロトコル (TCP/IP)** プロトコルはネットワーク接続のネットワーク アダプターのプロパティ内のコンポーネントとしてインストールします。
- **ftp**は対話的に使用できます。 起動すると、 **ftp** により、使用することができますサブ環境 **ftp** コマンドです。 」と入力して、コマンド プロンプトに返すことができます、 **終了** コマンドです。 ときに、 **ftp** サブ環境が実行されている場合で示された、 **ftp >** コマンド プロンプト。 詳細については、次を参照してください。、 **ftp** コマンドです。
- IPv6 プロトコルがインストールされている場合、 **ftp**は ipv6 の使用をサポートします。 詳細については、「[その他の参照](ftp.md#BKMK_additionalRef)情報」を参照してください。
  ## <a name="BKMK_Examples"></a>例
  Ftp.example.microsoft.com という名前の ftp サーバーにログオンするには、次のように入力します。
  ```
  ftp ftp.example.microsoft.com
  ```
  Ftp.example.microsoft.com という名前の ftp サーバーにログオンし、resync という名前のファイルに含まれている**ftp**コマンドを実行するには、次のように入力します。
  ```
  ftp -s:resync.txt ftp.example.microsoft.com
  ```
  ## <a name="BKMK_additionalRef"></a>その他の参照情報
- [IP バージョン6](https://technet.microsoft.com/library/cc738636(v=ws.10).aspx)
- [IPv6 アプリケーション](https://technet.microsoft.com/library/cc782509(v=ws.10).aspx)
- [コマンド ライン構文の記号](command-line-syntax-key.md)
