---
title: change logon
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c04eaffe366dce079aed53351589c1b5026954e3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379638"
---
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="change-logon"></a>change logon
クライアントセッションからのログオンを有効または無効にします。または、現在のログオンステータスを表示します。
このユーティリティは、システムのメンテナンスに役立ちます。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。
> ## <a name="syntax"></a>構文
> ```
> change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |     パラメーター      |                                                       説明                                                        |
> |--------------------|--------------------------------------------------------------------------------------------------------------------------|
> |       /query       |                             有効または無効になっているかどうかについて、現在のログオン状態を表示します。                              |
> |      /enable       |                              コンソールからではなく、クライアントセッションからのログオンを有効にします。                              |
> |      /disable      |  コンソールからではなく、クライアントセッションからの以降のログオンを無効にします。 現在ログオンしているユーザーには影響しません。   |
> |       /ドレイン       |                 新しいクライアントセッションからのログオンを無効にしますが、既存のセッションへの再使用を許可します。                 |
> | 再起動する (& a) | コンピューターが再起動されるまで新しいクライアントセッションからのログオンを無効にしますが、既存のセッションへの再実行を許可します。 |
> |         /?         |                                           コマンド プロンプトにヘルプを表示します。                                           |
> 
> ## <a name="remarks"></a>コメント
> - **[ログオンの変更]** コマンドを使用できるのは管理者だけです。
> - システムを再起動すると、ログオンが再度有効になります。 クライアントセッションからリモートデスクトップセッションホスト (rd セッションホスト) サーバーに接続し、ログオンを無効にしてからログオフしてからログオフすると、セッションに再接続できなくなります。 クライアントセッションからのログオンを再び有効にするには、コンソールでログオンします。
>   ## <a name="BKMK_examples"></a>例
> - 現在のログオン状態を表示するには、次のように入力します。
>   ```
>   change logon /query
>   ```
> - クライアントセッションからのログオンを有効にするには、次のように入力します。
>   ```
>   change logon /enable
>   ```
> - クライアントログオンを無効にするには、次のように入力します。
>   ```
>   change logon /disable
>   ```
>   #### <a name="additional-references"></a>その他の参照情報
>   [コマンドライン構文のキー](command-line-syntax-key.md)
>   [変更](change.md)
>   [リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
