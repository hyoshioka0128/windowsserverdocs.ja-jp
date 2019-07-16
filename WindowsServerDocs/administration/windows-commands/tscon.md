---
title: tscon
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 315a9793-cd10-4987-bb68-89a9d13f7fce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8cac59b2f5524df5a82e9c83424fd781f0ef7c8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440928"
---
# <a name="tscon"></a>tscon

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上の別のセッションに接続します。  
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。  

> [!NOTE]  
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。

## <a name="syntax"></a>構文  
```  
tscon {<SessionID> | <SessionName>} [/dest:<SessionName>] [/password:<pw> | /password:*] [/v]  
```  
## <a name="parameters"></a>パラメーター  

|パラメーター|説明|  
|-------|--------|  
|\<SessionID>|接続するセッションの ID を指定します。 オプションを使用する場合 **/dest:** <*SessionName*> パラメーターで接続するセッションの ID です。|  
|\<SessionName>|接続するセッションの名前を指定します。|  
|/dest:\<SessionName>|現在のセッションの名前を指定します。 新しいセッションに接続するときに、このセッションは切断されます。|  
|/password:\<pw>|接続するセッションを所有するユーザーのパスワードを指定します。 接続のユーザーがセッションを所有していないときに、このパスワードが必要です。|  
|/password: *|接続するセッションを所有するユーザーのパスワードを要求します。|  
|/v|実行する操作についての情報を表示します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>注釈  
-   フル コントロール アクセス許可があるか、別のセッションに接続するための特別なアクセス許可を接続する必要があります。  
-   **/Dest:** <*SessionName*> パラメーターでは、別のセッションに別のユーザーのセッションを接続することができます。  
-   パスワードを指定しない場合、<*パスワード*> パラメーター、および対象のセッションが現在のもの以外のユーザーに属している**tscon**は失敗します。  
-   コンソール セッションに接続することはできません。  

## <a name="BKMK_examples"></a>例  
- 現在の rd セッション ホスト サーバー上のセッション 12 への接続を現在のセッションの切断は、次のように入力します。  
  ```  
  tscon 12  
  ```  
- Mypass というパスワードを使用して、現在の rd セッション ホスト サーバー上のセッション 23 に接続を現在のセッションの切断は、次のように入力します。  
  ```  
  tscon 23 /password:mypass  
  ```  
- TERM05、という名前のセッションに TERM03 をという名前のセッションの接続を TERM05、セッションを切断が接続されている場合は、次のように入力します。  
  ```  
  tscon TERM03 /v /dest:TERM05  
  ```  
  #### <a name="additional-references"></a>その他の参照情報  
  [コマンド ライン構文の記号](command-line-syntax-key.md)  
  [リモート デスクトップ サービス&#40;ターミナル サービス&#41;コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)  
