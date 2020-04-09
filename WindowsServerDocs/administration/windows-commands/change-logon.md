---
title: change logon
description: クライアントセッションからのログオンを有効または無効にする、または現在のログオン状態を表示する change logon の Windows コマンドトピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a101fc567981716536ecad8e754b81a43eb2c91
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848155"
---
# <a name="change-logon"></a>change logon

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

クライアントセッションからのログオンを有効または無効にします。または、現在のログオンステータスを表示します。 このユーティリティは、システムのメンテナンスに役立ちます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
```
### <a name="parameters"></a>パラメーター

|     パラメーター      |                                                       説明                                                        |
|--------------------|--------------------------------------------------------------------------------------------------------------------------|
|       /query       |                             有効または無効になっているかどうかについて、現在のログオン状態を表示します。                              |
|      /enable       |                              コンソールからではなく、クライアントセッションからのログオンを有効にします。                              |
|      /disable      |  コンソールからではなく、クライアントセッションからの以降のログオンを無効にします。 現在ログオンしているユーザーには影響しません。   |
|       /ドレイン       |                 新しいクライアントセッションからのログオンを無効にしますが、既存のセッションへの再使用を許可します。                 |
| 再起動する (& a) | コンピューターが再起動されるまで新しいクライアントセッションからのログオンを無効にしますが、既存のセッションへの再実行を許可します。 |
|         /?         |                                           コマンド プロンプトでヘルプを表示します。                                           |

## <a name="remarks"></a>コメント
- **[ログオンの変更]** コマンドを使用できるのは管理者だけです。
- システムを再起動すると、ログオンが再度有効になります。 クライアントセッションからリモートデスクトップセッションホスト (rd セッションホスト) サーバーに接続し、ログオンを無効にしてからログオフしてからログオフすると、セッションに再接続できなくなります。 クライアントセッションからのログオンを再び有効にするには、コンソールでログオンします。

## <a name="examples"></a><a name=BKMK_examples></a>例

- 現在のログオン状態を表示するには、次のように入力します。
  ```
  change logon /query
  ```
- クライアントセッションからのログオンを有効にするには、次のように入力します。
  ```
  change logon /enable
  ```
- クライアントログオンを無効にするには、次のように入力します。
  ```
  change logon /disable
  ```
  
## <a name="additional-references"></a>その他の参照情報
- - [コマンド ライン構文の記号](command-line-syntax-key.md)
- [change](change.md)
- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
