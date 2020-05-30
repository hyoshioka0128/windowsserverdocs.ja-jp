---
title: tlntadmn
description: ローカルコンピューターまたはリモートコンピューターを管理し、telnet サーバーサービスを実行している tlntの管理のトピックを参照してください。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fcade72f7170e94463abb9b473d4c6bd2251f086
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222643"
---
# <a name="tlntadmn"></a>tlntadmn

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバーサービスを実行しているローカルコンピューターまたはリモートコンピューターを管理します。

## <a name="syntax"></a>構文
```
tlntadmn [<computerName>] [-u <UserName>] [-p <Password>] [{start | stop | pause | continue}] [-s {<SessionID> | all}] [-k {<SessionID> | all}] [-m {<SessionID> | all}  <Message>] [config [dom = <Domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <Connections>] [port = <Number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]
```
#### <a name="parameters"></a>パラメーター

|                   パラメーター                    |                                                                                                                                                       説明                                                                                                                                                        |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                \<computerName>                 |                                                                                                                    接続先のサーバーの名前を指定します。 既定はローカル コンピュータです。                                                                                                                    |
|         -u \<UserName> -p\<Password>          |                                                管理するリモートサーバーの管理者資格情報を指定します。 このパラメーターは、管理者資格情報でログオンしていないリモートサーバーを管理する場合に必要です。                                                |
|                     start                      |                                                                                                                                            telnet サーバーサービスを開始します。                                                                                                                                             |
|                      stop                      |                                                                                                                                             Telnet サーバーサービスを停止します。                                                                                                                                              |
|                     pause                      |                                                                                                                          telnet サーバーサービスを一時停止します。 新しい接続は受け付けられません。                                                                                                                          |
|                    continue                    |                                                                                                                                            Telnet サーバーサービスを再開します。                                                                                                                                            |
|          -s { \<SessionID> &#124; all}          |                                                                                                                                             アクティブな telnet セッションを表示します。                                                                                                                                             |
|          -k { \<SessionID> &#124; all}          |                                                                                                        Telnet セッションを終了します。 セッション ID を入力して特定のセッションを終了するか、[すべて] を入力してすべてのセッションを終了します。                                                                                                         |
|    -m { \<SessionID> &#124; all}<Message>     |                                                   1つ以上のセッションにメッセージを送信します。 セッション ID を入力して特定のセッションにメッセージを送信するか、[すべて] を入力してすべてのセッションにメッセージを送信します。 引用符で囲んで送信するメッセージを入力します。                                                   |
|             config dom =\<Domain>             |                                                                                                                                      サーバーの既定のドメインを構成します。                                                                                                                                       |
|      config ctrlakeymap マップ = {yes &#124; no}      |                                                                                     Telnet サーバーが CTRL + A を ALT として解釈するかどうかを指定します。 ショートカットキーをマップするには **「yes」** と入力し、マッピングを禁止するには「 **no** 」と入力します。                                                                                     |
|       構成のタイムアウト = \<hh> : \<mm>\<ss>       |                                                                                                                                 タイムアウト期間を時間、分、および秒で設定します。                                                                                                                                 |
|     config timeoutactive = {yes &#124; no      |                                                                                                                                            アイドル状態のセッションのタイムアウトを有効にします。                                                                                                                                             |
|          構成 maxfail =\<attempts>          |                                                                                                                          切断するまでのログオン失敗回数の最大値を設定します。                                                                                                                          |
|        構成 maxconn =\<Connections>         |                                                                                                                                         接続の最大数を設定します。                                                                                                                                          |
|            構成ポート = < \>             |                                                                                                                    Telnet ポートを設定します。 1024より小さい整数値を指定してポートを指定する必要があります。                                                                                                                    |
| config sec {+ &#124;-} NTLM {+ &#124;-} passwd | ログオン試行を認証するために NTLM とパスワードのどちらを使用するか、またはその両方を使用するかを指定します。 特定の種類の認証を使用するには、 **+** その認証の種類の前にプラス記号 () を入力します。 特定の種類の認証を使用しないようにするには、 **-** その認証の種類の前にマイナス記号 () を入力します。 |
|     config モード = {console &#124; stream}      |                                                                                                                                             操作のモードを指定します。                                                                                                                                             |
|                       -?                       |                                                                                                                                           コマンド プロンプトにヘルプを表示します。                                                                                                                                           |

## <a name="remarks"></a>解説
-   サーバーの設定を表示するには、パラメーターを指定せずに「 **tlntを**使用します。
-   **Tlntて n**コマンドを使用するには、管理者の資格情報を使用してローカルコンピューターにログオンする必要があります。 リモートコンピューターを管理するには、リモートコンピューターの管理者資格情報も指定する必要があります。 これを行うには、ローカルコンピューターとリモートコンピューターの両方の管理者資格情報を持つアカウントを使用してローカルコンピューターにログオンします。 この方法を使用できない場合は、 **-u**パラメーターと **-p**パラメーターを使用して、リモートコンピューターの管理者資格情報を指定できます。

## <a name="examples"></a>例
アイドルセッションタイムアウトを30分に設定します。
```
tlntadmn config timeout=0:30:0
```
アクティブな telnet セッションを表示します。
```
tlntadmn -s
```

## <a name="additional-references"></a>その他のリファレンス
-   [telnet 操作ガイド](https://technet.microsoft.com/library/cc753164(v=ws.10).aspx)
- [コマンド ライン構文の記号](command-line-syntax-key.md)
