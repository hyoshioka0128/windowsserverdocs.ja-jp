---
title: ftp
description: Ftp コマンドのリファレンストピックです。このコマンドは、ファイル転送プロトコル (ftp) サーバーサービスを実行しているコンピューターとの間でファイルを転送します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 758335e1-fd8d-448c-a654-993126239dd9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3920306ce05aeb1b1e364c8146c461ea187f6560
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820242"
---
# <a name="ftp"></a>ftp

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル転送プロトコル (ftp) サーバーサービスを実行しているコンピューターとの間でファイルを転送します。 このコマンドは、ASCII テキストファイルを処理することによって、対話形式またはバッチモードで使用できます。

## <a name="syntax"></a>構文

```
ftp [-v] [-d] [-i] [-n] [-g] [-s:<filename>] [-a] [-A] [-x:<sendbuffer>] [-r:<recvbuffer>] [-b:<asyncbuffers>][-w:<windowssize>][<host>] [-?]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ----------| ----------- |
| -v | リモート サーバーの応答を表示をしません。 |
| -d | デバッグを有効にし、FTP クライアントと FTP サーバーの間で渡されたすべてのコマンドを表示します。 |
| -i | 複数のファイル転送中の対話形式のプロンプトを無効にします。 |
| -n | 初期接続時に自動ログインを抑制します。 |
| -g | ファイル名グロビングを無効にします。  **Glob** ローカル ファイルとパス名にワイルドカード文字としてアスタリスク (*) と疑問符 (?) の使用を許可します。 |
| 2$s`<filename>` | 含むテキスト ファイルを指定 **ftp** コマンドです。 これらのコマンドを実行した後に自動的に **ftp** を開始します。 このパラメーターには、スペースは許可されません。 リダイレクトではなく、このパラメーターを使用して (`<`)。 **注:** Windows 8 および Windows Server 2012 以降のオペレーティング システムでは、utf-8 でテキスト ファイルが書き込まれる必要があります。 |
| -a | Ftp データ接続をバインドするときに、任意のローカルインターフェイスを使用できることを指定します。 |
| -A | Ftp サーバーに匿名でログオンします。 |
| 閉じる`<sendbuffer> `| 8192 の既定の SO_SNDBUF サイズをオーバーライドします。 |
| \r\n\r\n`<recvbuffer>` | 8192 の既定の SO_RCVBUF サイズをオーバーライドします。 |
| b`<asyncbuffers>` | 3 の既定の非同期バッファー数をオーバーライドします。 |
| リダイレクト`<windowssize>` | 転送バッファーのサイズを指定します。 既定のウィンドウ サイズは、4096 バイトです。 |
| `<host>` | 接続先の ftp サーバーのコンピューター名、IP アドレス、または IPv6 アドレスを指定します。 ホスト名またはアドレスを指定した場合は、行の最後のパラメーターになる可能性があります。 |
| -? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- **Ftp**のコマンドラインパラメーターでは、大文字と小文字が区別されます。

- このコマンドは、使用可能な場合にのみ、 **インターネット プロトコル (TCP/IP)** プロトコルはネットワーク接続のネットワーク アダプターのプロパティ内のコンポーネントとしてインストールします。

- **Ftp**コマンドは対話形式で使用できます。 起動すると、 **ftp** により、使用することができますサブ環境 **ftp** コマンドです。 」と入力して、コマンド プロンプトに返すことができます、 **終了** コマンドです。 **Ftp**サブ環境が実行されている場合は、コマンドプロンプトによって示され `ftp >` ます。 詳細については、 **ftp**コマンドを参照してください。

- **Ftp**コマンドは、ipv6 プロトコルがインストールされている場合に ipv6 の使用をサポートします。

### <a name="examples"></a>例

という名前の ftp サーバーにログオンするには `ftp.example.microsoft.com` 、次のように入力します。

```
ftp ftp.example.microsoft.com
```

という名前の ftp サーバーにログオン `ftp.example.microsoft.com` し、 *resync*という名前のファイルに含まれている**ftp**コマンドを実行するには、次のように入力します。

```
ftp -s:resync.txt ftp.example.microsoft.com
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))

- [IP バージョン 6](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc738636(v=ws.10))

- [IPv6 アプリケーション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc782509(v=ws.10))
