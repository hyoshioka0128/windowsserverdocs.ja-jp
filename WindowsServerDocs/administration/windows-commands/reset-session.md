---
title: reset session
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 67a4e910ba87209c9700f2242f7859a6cc9e725f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384527"
---
# <a name="reset-session"></a>reset session

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のセッションをリセット (削除) できます。  
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。  

> [!NOTE]  
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。  

## <a name="syntax"></a>構文  
```  
reset session {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]  
```  

## <a name="parameters"></a>パラメーター  

|パラメーター|説明|  
|-------|--------|  
|\<のセッション >|リセットするセッションの名前を指定します。 セッションの名前を確認するのには、使用、 **クエリ セッション** コマンドです。|  
|\<SessionID >|リセットするセッションの ID を指定します。|  
|/server:\<ServerName >|リセットするセッションに含まれる、ターミナル サーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。|  
|/v|実行されているアクションに関する情報を表示します。|  
|/?|コマンド プロンプトにヘルプを表示します。|  

## <a name="remarks"></a>注釈  
-   常に自身のセッションをリセットすることができますが、別のユーザーのセッションをリセットするフル コントロール アクセス許可を持つ必要があります。  
-   セッションでデータが失われると、ユーザーに警告せずにユーザーのセッションをリセットすることができますを注意してください。  
-   セッションをリセットする必要がありますのみが正しく動作しないか、または場合に、応答を停止しています。  
-   **/Server** パラメーターは、使用する場合にのみ必要 **セッションをリセット** リモート サーバーからです。  

## <a name="BKMK_examples"></a>例  
- Rdp-tcp 6 を指定されたセッションをリセットするには、次のように入力します。  
  ```  
  reset session rdp-tcp#6  
  ```  
- セッション ID が 3 を使用して、セッションをリセットするには、次のように入力します。  
  ```  
  reset session 3  
  ```  

#### <a name="additional-references"></a>その他の参照情報  
[コマンド ライン構文の記号](command-line-syntax-key.md)  
[リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)  
