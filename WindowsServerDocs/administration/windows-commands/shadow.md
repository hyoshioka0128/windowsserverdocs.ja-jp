---
title: shadow
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 125b2971d5d4783ea0b974c45b988cbd1c58a2bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877113"
---
# <a name="shadow"></a>shadow

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上の別のユーザーのアクティブなセッションをリモートで制御できます。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<SessionName>|リモートで制御するセッションの名前を指定します。|
|\<SessionID>|リモートで制御するセッションの ID を指定します。 使用 **クエリ ユーザー** セッションとのセッション Id の一覧を表示します。|
|/server:\<ServerName >|リモートで制御するセッションを格納している rd セッション ホスト サーバーを指定します。 既定では、現在の rd セッション Host4 サーバーが使用されます。|
|/v|実行する操作についての情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   表示するか、セッションをアクティブに制御します。 ユーザーのセッションをアクティブに制御を選択した場合は、キーボード入力やマウスの操作をセッションにことができます。
-   (現在のセッション) を除く自身のセッションをいつでもリモートで制御できますが、フル コントロール アクセス許可または別のセッションをリモートで制御する特殊アクセス許可をリモート制御する必要があります。
-   リモート デスクトップ サービス マネージャーを使用して、リモート_コントロールを開始することもできます。
-   監視を開始する前に、サーバーは、セッションは、この警告が無効になっている場合を除き、リモートで制御されようしようとしていますが、ユーザーに警告します。 セッションは、ユーザーからの応答を待機している間は、数秒以内に停止したように見える場合があります。 ユーザーとセッションのリモート制御を構成するには、リモート デスクトップ サービスの構成ツールまたはリモート デスクトップ サービスの拡張機能をローカル ユーザーとグループと active directory ユーザーとコンピュータを使用します。
-   セッションがリモートで制御または操作が失敗したセッションで使用されるビデオの解像度をサポートできる必要があります。
-   コンソール セッションもリモートで制御できます別のセッションも、リモートで使用して制御できる別のセッション。
-   (シャドウ) リモート制御を終了する場合は、ctrl キーを押します。 * (を使用して \* テンキーのみ)。

## <a name="BKMK_examples"></a>例
-   セッション 93 をシャドウする次のように入力します。
    ```
    shadow 93
    ```
-   セッション ACCTG01 をシャドウするには、次のように入力します。
    ```
    shadow ACCTG01
    ```

#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
[リモート デスクトップ サービス(ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
