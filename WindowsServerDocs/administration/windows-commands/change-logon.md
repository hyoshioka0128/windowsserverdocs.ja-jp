---
title: change logon
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 45c171a1b14cf69abf039d57697cad933a2dd87b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434571"
---
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="change-logon"></a>change logon
有効またはクライアントのセッションからのログオンを無効にします。 または現在のログオン状態を表示します。
このユーティリティは、システム メンテナンスのために便利です。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
> ## <a name="syntax"></a>構文
> ```
> change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |     パラメーター      |                                                       説明                                                        |
> |--------------------|--------------------------------------------------------------------------------------------------------------------------|
> |       /query       |                             有効または無効になっているかどうかは、現在のログオン状態を表示します。                              |
> |      /enable       |                              コンソールからではなく、クライアント セッションからのログオンを有効にします。                              |
> |      /disable      |  コンソールからではなく、クライアント セッションからそれ以降のログオンを無効にします。 現在ログオンしているユーザーには影響しません。   |
> |       /drain       |                 新しいクライアント セッションからのログオンを無効にしますが、既存のセッションに再接続を許可します。                 |
> | /drainuntilrestart | コンピューターが再起動により、既存のセッションに再接続されるまで、新しいクライアント セッションからのログオンを無効にします。 |
> |         /?         |                                           コマンド プロンプトにヘルプを表示します。                                           |
> 
> ## <a name="remarks"></a>注釈
> - 管理者のみが使用できる、**ログオン変更**コマンド。
> - ログオンには、システムを再起動するときに再び有効にします。 ログオンを無効にするクライアント セッションからリモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーに接続しているし、再びログオンを有効にする前にログオフし、セッションに再接続することはできません。 クライアント セッションからのログオンを再度有効にするには、するには、コンソールにログオンします。
>   ## <a name="BKMK_examples"></a>例
> - 現在のログオン状態を表示するには、次のように入力します。
>   ```
>   change logon /query
>   ```
> - クライアント セッションからのログオンを有効にするには、次のように入力します。
>   ```
>   change logon /enable
>   ```
> - クライアントのログオンを無効にするには、次のように入力します。
>   ```
>   change logon /disable
>   ```
>   #### <a name="additional-references"></a>その他の参照
>   [コマンドライン構文のポイント](command-line-syntax-key.md)
>   [変更](change.md)
>   [Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
