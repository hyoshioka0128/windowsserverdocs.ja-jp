---
title: reset session
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4f029ecc-874e-415a-95a8-8b731bae35f9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: df7b953e02c7339b7ed66a831955f802dd21e624
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722359"
---
# <a name="reset-session"></a>reset session

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のセッションをリセット (削除) できます。  
  

> [!NOTE]  
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。  

## <a name="syntax"></a>構文  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

### <a name="parameters"></a>パラメーター  

|パラメーター|[説明]|  
|-------|--------|  
|\<セッション名>|リセットするセッションの名前を指定します。 セッションの名前を確認するのには、使用、 **クエリ セッション** コマンドです。|  
|\<SessionID>|リセットするセッションの ID を指定します。|  
|/server:\<ServerName>|リセットするセッションに含まれる、ターミナル サーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。|  
|/v|実行されているアクションに関する情報を表示します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>Remarks  
-   常に自身のセッションをリセットすることができますが、別のユーザーのセッションをリセットするフル コントロール アクセス許可を持つ必要があります。  
-   セッションでデータが失われると、ユーザーに警告せずにユーザーのセッションをリセットすることができますを注意してください。  
-   セッションをリセットする必要がありますのみが正しく動作しないか、または場合に、応答を停止しています。  
-   **/Server** パラメーターは、使用する場合にのみ必要 **セッションをリセット** リモート サーバーからです。  

## <a name="examples"></a>例  
- Rdp-tcp 6 を指定されたセッションをリセットするには、次のように入力します。  
  ```  
  reset session rdp-tcp#6  
  ```  
- セッション ID が 3 を使用して、セッションをリセットするには、次のように入力します。  
  ```  
  reset session 3  
  ```  

## <a name="additional-references"></a>その他のリファレンス  
- [コマンド ライン構文の記号](command-line-syntax-key.md)  
[リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)  
