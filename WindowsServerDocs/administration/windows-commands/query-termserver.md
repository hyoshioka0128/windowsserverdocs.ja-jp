---
title: クエリ termserver
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5baab78f6a7222bad121773e686bacb01dc8872a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817233"
---
# <a name="query-termserver"></a>クエリ termserver

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ネットワーク上のすべてのリモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーの一覧を表示します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
## <a name="syntax"></a>構文
```
query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<ServerName>|Rd セッション ホスト サーバーを識別する名前を指定します。|
|/domain:<Domain>|ターミナル サーバーを照会するドメインを指定します。 現在作業しているドメインを照会する場合は、ドメインを指定する必要はありません。|
|/address|各サーバーのネットワークとノードのアドレスを表示します。|
|続行/|情報の各画面が表示された後の一時停止できないようにします。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   **クエリ termserver**ネットワーク接続されている rd セッション ホスト サーバーと、次の情報を返しますのすべてを検索します。
    -   サーバーの名前
    -   ネットワーク (およびノード アドレス/address オプションを使用する場合)
## <a name="BKMK_examples"></a>例
-   ネットワーク上のすべての rd セッション ホスト サーバーに関する情報を表示するには、次のように入力します。
    ```
    query termserver
    ```
-   Server3 という名前の rd セッション ホスト サーバーに関する情報を表示するには、次のように入力します。
    ```
    query termserver Server3
    ```
-   CONTOSO ドメインですべての rd セッション ホスト サーバーに関する情報を表示するには、次のように入力します。
    ```
    query termserver /domain:CONTOSO
    ```
-   Server3 という名前の rd セッション ホスト サーバーのネットワークとノードのアドレスを表示するには、次のように入力します。
    ```
    query termserver Server3 /address
    ```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[クエリ](query.md)
[Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
