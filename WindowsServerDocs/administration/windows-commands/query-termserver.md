---
title: クエリ termserver
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8a0a4608a16df0336b90ea5df281278ae47a503
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722703"
---
# <a name="query-termserver"></a>クエリ termserver

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ネットワーク上のすべてのリモートデスクトップセッションホスト (rd セッションホスト) サーバーの一覧を表示します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。
> ## <a name="syntax"></a>構文
> ```
> query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
> ```
> ### <a name="parameters"></a>パラメーター
> 
> |    パラメーター     |                                                                        [説明]                                                                         |
> |------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |   <ServerName>   |                                               Rd セッションホストサーバーを識別する名前を指定します。                                               |
> | /domain<Domain> | ターミナル サーバーを照会するドメインを指定します。 現在作業しているドメインを照会する場合は、ドメインを指定する必要はありません。 |
> |     /address     |                                                  各サーバーのネットワークとノードのアドレスを表示します。                                                  |
> |    続行/     |                                              情報の各画面が表示された後の一時停止できないようにします。                                               |
> |        /?        |                                                            コマンド プロンプトにヘルプを表示します。                                                            |
> 
> ## <a name="remarks"></a>Remarks
> - **query termserver**は、接続されているすべての Rd セッションホストサーバーのネットワークを検索し、次の情報を返します。
>   - サーバーの名前
>   - ネットワーク (およびノード アドレス/address オプションを使用する場合)
>     ## <a name="examples"></a>例
> - ネットワーク上のすべての rd セッションホストサーバーに関する情報を表示するには、次のように入力します。
>   ```
>   query termserver
>   ```
> - Server3 という名前の rd セッションホストサーバーに関する情報を表示するには、次のように入力します。
>   ```
>   query termserver Server3
>   ```
> - ドメイン CONTOSO 内のすべての rd セッションホストサーバーに関する情報を表示するには、次のように入力します。
>   ```
>   query termserver /domain:CONTOSO
>   ```
> - Server3 という名前の rd セッションホストサーバーのネットワークとノードのアドレスを表示するには、次のように入力します。
>   ```
>   query termserver Server3 /address
>   ```
>   ## <a name="additional-references"></a>その他のリファレンス
>   - [コマンドライン構文キー](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [リモートデスクトップサービス (ターミナルサービス) コマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
