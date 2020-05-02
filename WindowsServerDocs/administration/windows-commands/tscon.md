---
title: tscon
description: リモートデスクトップセッションホスト (rd セッションホスト) サーバー上の別のセッションに接続する tscon のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a95b7b63f91e7450d949ded294a48c2596e385db
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721271"
---
# <a name="tscon"></a>tscon

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホストサーバー上の別のセッションに接続します。  

  

> [!NOTE]  
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。  

## <a name="syntax"></a>構文  
```  
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]  
```  
### <a name="parameters"></a>パラメーター  

|パラメーター|[説明]|  
|-------|--------|  
|\<SessionID>|接続先のセッションの ID を指定します。 省略可能な **/dest:**<*> パラメーター*を使用すると、これは接続先のセッションの ID になります。|  
|\<セッション名>|接続先のセッションの名前を指定します。|  
|/dest:\<セッション名>|現在のセッションの名前を指定します。 新しいセッションに接続すると、このセッションは切断されます。|  
|/password:\<pw>|接続先のセッションを所有するユーザーのパスワードを指定します。 このパスワードは、接続しているユーザーがセッションを所有していない場合に必要です。|  
|/password: *|接続先のセッションを所有するユーザーのパスワードの入力を求めます。|  
|/v|実行されているアクションに関する情報を表示します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>Remarks  
-   別のセッションに接続するには、フルコントロールアクセス許可を持っているか、特殊なアクセス許可を接続している必要があります。  
-   **/Dest:**<*の> パラメーター*を使用すると、別のユーザーのセッションを別のセッションに接続できます。  
-   <*password*> パラメーターにパスワードを指定せず、ターゲットセッションが現在のセッション以外のユーザーに属している場合、 **tscon**は失敗します。  
-   コンソールセッションに接続することはできません。  

## <a name="examples"></a>例  
- 現在の rd セッションホストサーバーのセッション12に接続し、現在のセッションを切断するには、次のように入力します。  
  ```  
  tscon 12  
  ```  
- 現在の rd セッションホストサーバーのセッション23に接続するには、パスワード mypass 使用して、現在のセッションを切断し、次のように入力します。  
  ```  
  tscon 23 /password:mypass  
  ```  
- TERM03 という名前のセッションを TERM05 という名前のセッションに接続し、セッション TERM05 を切断します。接続されている場合は、次のように入力します。  
  ```  
  tscon TERM03 /v /dest:TERM05  
  ```  
  ## <a name="additional-references"></a>その他のリファレンス  
  - [コマンド ライン構文の記号](command-line-syntax-key.md)  
  [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)  
