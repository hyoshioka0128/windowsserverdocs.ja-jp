---
title: ログオフ
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1661a9dd6cc89ea05980fd9085aa8fa67b8fe2c0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840415"
---
# <a name="logoff"></a>ログオフ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のセッションからユーザーをログオフし、そのセッションをサーバーから削除します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
logoff [<SessionName> | <SessionID>] [/server:<ServerName>] [/v]
```
### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                             説明                                                                              |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <SessionName>     |                                                                  セッションの名前を指定します。                                                                  |
|     <SessionID>      |                                                 サーバーに対するセッションを識別する数値 ID を指定します。                                                 |
| /server:<ServerName> | ユーザーがログオフするセッションを含む rd セッションホストサーバーを指定します。 指定しない場合は、現在アクティブになっているサーバーが使用されます。 |
|          /v          |                                                       実行されているアクションに関する情報を表示します。                                                        |
|          /?          |                                                                 コマンド プロンプトでヘルプを表示します。                                                                 |

## <a name="remarks"></a>コメント
- 現在ログオンしているセッションから、いつでもログオフできます。 ただし、他のセッションからユーザーをログオフするには、フルコントロールアクセス許可を持っている必要があります。
- 警告なしでセッションからユーザーをログオフすると、ユーザーのセッションでデータが失われる可能性があります。 この操作を実行する前に、 **msg**コマンドを使用してユーザーに警告するメッセージをユーザーに送信する必要があります。
- < SessionID > また*は < の* *SessionID*> が指定されていない場合、**ログオフ**すると、現在のセッションからユーザーからログオフされます。 < の*セッション名*> を指定する場合は、アクティブなものである必要があります。
- ユーザーをログオフすると、すべてのプロセスが終了し、セッションがサーバーから削除されます。
- コンソールセッションからユーザーをログオフすることはできません。
  ## <a name="examples"></a><a name=BKMK_examples></a>例
- 現在のセッションからユーザーをログオフするには、次のように入力します。
  ```
  logoff
  ```
- セッションの ID (例: セッション 12) を使用してセッションからユーザーをログオフするには、次のように入力します。
  ```
  logoff 12
  ```
- セッションとサーバーの名前を使用してセッションからユーザーをログオフするには (たとえば、Server1 の session TERM04)、次のように入力します。
  ```
  logoff TERM04 /server:Server1
  ```

## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
