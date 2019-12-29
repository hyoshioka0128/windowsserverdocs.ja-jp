---
title: クエリ termserver
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 95a2e102a147bd7ebee24995d1e1fcd4147f8174
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371892"
---
# <a name="query-termserver"></a>クエリ termserver

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ネットワーク上のすべてのリモートデスクトップセッションホスト (rd セッションホスト) サーバーの一覧を表示します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。
> ## <a name="syntax"></a>構文
> ```
> query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |    パラメーター     |                                                                        説明                                                                         |
> |------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |   <ServerName>   |                                               Rd セッションホストサーバーを識別する名前を指定します。                                               |
> | /domain: <Domain> | ターミナル サーバーを照会するドメインを指定します。 現在作業しているドメインを照会する場合は、ドメインを指定する必要はありません。 |
> |     /address     |                                                  各サーバーのネットワークとノードのアドレスを表示します。                                                  |
> |    続行/     |                                              情報の各画面が表示された後の一時停止できないようにします。                                               |
> |        /?        |                                                            コマンド プロンプトにヘルプを表示します。                                                            |
> 
> ## <a name="remarks"></a>コメント
> - **query termserver**は、接続されているすべての Rd セッションホストサーバーのネットワークを検索し、次の情報を返します。
>   - サーバーの名前
>   - ネットワーク (およびノード アドレス/address オプションを使用する場合)
>     ## <a name="BKMK_examples"></a>例
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
>   #### <a name="additional-references"></a>その他の参照情報
>   [コマンドライン構文のキー](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
