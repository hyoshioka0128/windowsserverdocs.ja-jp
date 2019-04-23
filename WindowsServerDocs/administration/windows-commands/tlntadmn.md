---
title: tlntadmn
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c321c4ebcaf5fbbae30f6825fef18b478554f665
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884193"
---
# <a name="tlntadmn"></a>tlntadmn

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Telnet サーバー サービスを実行しているローカルまたはリモート コンピューターを管理します。   
## <a name="syntax"></a>構文  
```  
tlntadmn [<computerName>] [-u <UserName>] [-p <Password>] [{start | stop | pause | continue}] [-s {<SessionID> | all}] [-k {<SessionID> | all}] [-m {<SessionID> | all}  <Message>] [config [dom = <Domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <Connections>] [port = <Number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|\<computerName>|接続するサーバーの名前を指定します。 既定はローカル コンピュータです。|  
|-u \<UserName> -p \<Password>|管理するリモート サーバーの管理者資格情報を指定します。 先をログオンしていない管理者資格情報でリモート サーバーを管理する場合、このパラメーターが必要です。|  
|start|telnet サーバー サービスを開始します。|  
|stop|Telnet サーバー サービスを停止します。|  
|pause|telnet サーバー サービスを一時停止します。 新しい接続は受け入れられません。|  
|続行|Telnet サーバー サービスを再開します。|  
|-s {\<SessionID> &#124; all}|アクティブな telnet セッションを表示します。|  
|-k {\<SessionID> &#124; all}|Telnet セッションを終了します。 特定のセッションを終了するセッション ID を入力するか、すべてのセッションを終了するすべてを入力します。|  
|-m {\<SessionID> &#124; all}  <Message>|1 つまたは複数のセッションにメッセージを送信します。 特定のセッションにメッセージを送信するセッション ID を入力するか、すべてのセッションにメッセージを送信するすべての入力します。 引用符の間で送信するメッセージを入力します。|  
|config dom =\<ドメイン >|サーバーの既定のドメインを構成します。|  
|config ctrlakeymap = {yes &#124; no}|Telnet サーバーで alt キーと CTRL + A を解釈するかどうかを指定します。 型**はい**マップのショートカット キー、または型に**ありません**マップを禁止します。|  
|config timeout = \<hh>:\<mm>:\<ss>|時間、分、および秒でタイムアウト期間を設定します。|  
|config timeoutactive = {yes &#124; no|アイドル セッションのタイムアウトを有効にします。|  
|config maxfail = \<attempts>|切断する前に失敗したログオン試行の最大数を設定します。|  
|config maxconn = \<Connections>|接続の最大数を設定します。|  
|ポートの構成 < \Number > =|Telnet ポートを設定します。 1024 より小さい整数では、ポートを指定する必要があります。|  
|config sec {+ &#124; -}NTLM {+ &#124; -}passwd|ログオン試行の認証に NTLM、パスワード、またはその両方を使用するかどうかを指定します。 特定の種類の認証を使用するには、プラス記号を入力 (**+**) 認証の種類の前にします。 特定の種類の認証の使用を防ぐためには、マイナス記号を入力します (**-**) 認証の種類の前にします。|  
|config mode = {console &#124; stream}|操作モードを指定します。|  
|-?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>注釈  
-   サーバーの設定を表示するには、次のように入力します。 **tlntadmn**パラメーターなし。  
-   使用する、 **tlntadmn**コマンドを管理者の資格情報を使ってローカル コンピューターにログオンする必要があります。 リモート コンピューターを管理するには、リモート コンピューターの管理者の資格情報を指定することもあります。 ローカル コンピューターとリモート コンピューターの両方の管理者の資格情報を持つアカウントを使用して、ローカル コンピューターにログオンすることで行うことができます。 このメソッドを使用することはできない場合、は、使用、 **-u**と **-p**リモート コンピューターの管理者の資格情報を提供するパラメーター。  

## <a name="BKMK_Examples"></a>例  
30 分にアイドル状態のセッション タイムアウトを構成します。  
```  
tlntadmn config timeout=0:30:0  
```  
アクティブな telnet セッションを表示します。  
```  
tlntadmn -s  
```  

## <a name="additional-references"></a>その他の参照情報  
-   [telnet の操作ガイド](https://technet.microsoft.com/library/cc753164(v=ws.10).aspx)  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
