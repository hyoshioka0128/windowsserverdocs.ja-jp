---
title: shadow
description: Shadow の Windows コマンドに関するトピック。リモートデスクトップセッションホストサーバー上の別のユーザーのアクティブなセッションをリモートで制御できます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f81d9717-6883-4e14-9508-4b2a87e48ea7 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90c3202d810257cc94c73b88c5c1627901f54af0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834335"
---
# <a name="shadow"></a>shadow

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

では、リモートデスクトップセッションホストサーバー上の別のユーザーのアクティブなセッションをリモートで制御できます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<のセッション >|リモートで制御するセッションの名前を指定します。|
|\<SessionID >|リモートで制御するセッションの ID を指定します。 使用 **クエリ ユーザー** セッションとのセッション Id の一覧を表示します。|
|/server:\<ServerName >|リモートで制御するセッションを含む rd セッションホストサーバーを指定します。 既定では、現在の rd セッション Host4 サーバーが使用されます。|
|/v|実行されているアクションに関する情報を表示します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント
-   セッションを表示したり、セッションをアクティブに制御することができます。 ユーザー セッションをアクティブに制御する場合は、セッションに対してキーボードとマウスによる操作を入力することができます。
-   (現在のセッションを除く) いつでも独自のセッションをリモートで制御できますが、別のセッションをリモートで制御するには、フルコントロールアクセス許可またはリモートコントロールの特別なアクセス許可が必要です。
-   リモート デスクトップ サービス マネージャーを使用して、リモート_コントロールを開始することもできます。
-   監視を始める前に、セッションがリモートで制御されようとしていることが、サーバーからユーザーに警告されます。ただし、警告が無効になっている場合を除きます。 ユーザーからの応答を待っている間、セッションが数秒間停止したように見えることがあります。 ユーザーとセッションのリモートコントロールを構成するには、リモートデスクトップサービス構成ツール、または [ローカルユーザーとグループ] と [active directory ユーザーとコンピューター] のリモートデスクトップサービス拡張機能を使用します。
-   制御する側のセッションでは、リモートで制御されるセッションでのビデオ解像度をサポートできる必要があります。サポートできない場合は、操作に失敗します。
-   コンソール セッションもリモートで制御できます別のセッションも、リモートで使用して制御できる別のセッション。
-   リモートコントロール (シャドウ) を終了する場合は、CTRL +\* キーを押します (テンキーの \* を使用します)。

## <a name="examples"></a><a name=BKMK_examples></a>例
-   セッション 93 をシャドウする次のように入力します。
    ```
    shadow 93
    ```
-   セッション ACCTG01 をシャドウするには、次のように入力します。
    ```
    shadow ACCTG01
    ```

## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
