---
title: reset session
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6510f8b21186b856eb489c1add0674b8984b0e56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857093"
---
# <a name="reset-session"></a>reset session

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上のセッションのリセット (削除) できます。  
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。  

> [!NOTE]  
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。  

## <a name="syntax"></a>構文  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|\<SessionName>|リセットするセッションの名前を指定します。 セッションの名前を確認するのには、使用、 **クエリ セッション** コマンドです。|  
|\<SessionID>|リセットするセッションの ID を指定します。|  
|/server:\<ServerName >|リセットするセッションに含まれる、ターミナル サーバーを指定します。 それ以外の場合、現在の rd セッション ホスト サーバーが使用されます。|  
|/v|実行する操作についての情報を表示します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>注釈  
-   常に自身のセッションをリセットすることができますが、別のユーザーのセッションをリセットするフル コントロール アクセス許可を持つ必要があります。  
-   セッションでデータが失われると、ユーザーに警告せずにユーザーのセッションをリセットすることができますを注意してください。  
-   セッションをリセットする必要がありますのみが正しく動作しないか、または場合に、応答を停止しています。  
-   **/Server** パラメーターは、使用する場合にのみ必要 **セッションをリセット** リモート サーバーからです。  

## <a name="BKMK_examples"></a>例  
-   Rdp-tcp 6 を指定されたセッションをリセットするには、次のように入力します。  
    ```  
    reset session rdp-tcp#6  
    ```  
-   セッション ID が 3 を使用して、セッションをリセットするには、次のように入力します。  
    ```  
    reset session 3  
    ```  

#### <a name="additional-references"></a>その他の参照情報  
[コマンドライン構文キー](command-line-syntax-key.md)  
[リモート デスクトップ サービス&#40;ターミナル サービス&#41;コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)  
