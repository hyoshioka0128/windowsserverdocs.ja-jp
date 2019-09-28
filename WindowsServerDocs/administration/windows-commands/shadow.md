---
title: shadow
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f81d9717-6883-4e14-9508-4b2a87e48ea7 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb2fad4b0a553e736755f2dc56e5d88297a1fef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383961"
---
# <a name="shadow"></a>shadow

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

では、リモートデスクトップセッションホスト (rd セッションホスト) サーバー上の別のユーザーのアクティブなセッションをリモートで制御できます。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|@no__t ~ 0SessionName セッション >|リモートで制御するセッションの名前を指定します。|
|\<SessionID >|リモートで制御するセッションの ID を指定します。 使用 **クエリ ユーザー** セッションとのセッション Id の一覧を表示します。|
|/server: @no__t 0ServerName >|リモートで制御するセッションを含む rd セッションホストサーバーを指定します。 既定では、現在の rd セッション Host4 サーバーが使用されます。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント
-   表示するか、セッションをアクティブに制御します。 ユーザーのセッションをアクティブに制御を選択した場合は、キーボード入力やマウスの操作をセッションにことができます。
-   (現在のセッションを除く) いつでも独自のセッションをリモートで制御できますが、別のセッションをリモートで制御するには、フルコントロールアクセス許可またはリモートコントロールの特別なアクセス許可が必要です。
-   リモート デスクトップ サービス マネージャーを使用して、リモート_コントロールを開始することもできます。
-   監視を開始する前に、サーバーは、セッションは、この警告が無効になっている場合を除き、リモートで制御されようしようとしていますが、ユーザーに警告します。 セッションは、ユーザーからの応答を待機している間は、数秒以内に停止したように見える場合があります。 ユーザーとセッションのリモートコントロールを構成するには、リモートデスクトップサービス構成ツール、または [ローカルユーザーとグループ] と [active directory ユーザーとコンピューター] のリモートデスクトップサービス拡張機能を使用します。
-   セッションがリモートで制御または操作が失敗したセッションで使用されるビデオの解像度をサポートできる必要があります。
-   コンソール セッションもリモートで制御できます別のセッションも、リモートで使用して制御できる別のセッション。
-   リモートコントロール (シャドウ) を終了する場合は、CTRL + \* キーを押します (テンキーの \* を使用します)。

## <a name="BKMK_examples"></a>例
-   セッション 93 をシャドウする次のように入力します。
    ```
    shadow 93
    ```
-   セッション ACCTG01 をシャドウするには、次のように入力します。
    ```
    shadow ACCTG01
    ```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](command-line-syntax-key.md)
[リモート デスクトップ サービス(ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
