---
title: tcmsetup
description: TAPI クライアントを設定および無効にする方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15e0c10f-996f-4301-92e5-943f7ee8212d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbfc9a0238d258f11233b0e48a30048c1d62cef4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833415"
---
# <a name="tcmsetup"></a>tcmsetup



設定または、TAPI クライアントを無効にします。

## <a name="syntax"></a>構文

```
tcmsetup [/q] [/x] /c <Server1> [<Server2> …] 
tcmsetup  [/q] /c /d
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/q|メッセージ ボックスが表示されないようにします。|
|/x|大量のトラフィックがあるためパケット損失が多いネットワークでは接続指向のコールバックを使用するよう指定します。 このパラメーターを省略すると、コネクションレス型コールバックが使用されます。|
|/c|必須。 クライアントのセットアップを指定します。|
|\<Server1 >|必須。 クライアントで使用される TAPI サービス プロバイダーのあるリモート サーバーの名前を指定します。 クライアントはサービス プロバイダーの回線や電話を使用します。 クライアントは、指定するサーバーと同じドメイン内、またはそのサーバーがあるドメインと双方向の信頼関係が確立されているドメイン内に存在する必要があります。|
|Server2 > を \<しています...|このクライアントで利用できる追加のサーバーがあれば、それらを指定します。 複数のサーバーを指定する場合は、サーバー名の間をスペースで区切ります。|
|/d|リモート サーバーの一覧をクリアします。 TAPI クライアントがリモート サーバー上の TAPI サービス プロバイダーを使用できないようにすることで、クライアントを無効にします。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   この手順を実行するには、ローカル コンピューターの Administrators グループのメンバーであるか、適切な権限が委任されている必要があります。 コンピューターがドメインに参加している場合、Domain Admins グループのメンバーはこの手順を実行できる可能性があります。 セキュリティの点から、 **[別のユーザーとして実行]** を使用してこの手順を実行することを検討してください。
-   TAPI が正しく機能するためには、実行する必要があります **tcmsetup** TAPI クライアントによって使用されるリモート サーバーを指定します。
-   クライアント ユーザーは、TAPI サーバー上、電話または回線を使用できるように、テレフォニー サーバーの管理者は、電話または回線にユーザーを割り当てる必要があります。
-   このコマンドで作成されるテレフォニー サーバーの一覧により、クライアントで利用できるテレフォニー サーバーを示す既存の一覧はすべて置き換えられます。 このコマンドで既存の一覧にサーバーを追加することはできません。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[コマンドシェルの概要](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)

[クライアントコンピューターのテレフォニーサーバーを指定する](https://technet.microsoft.com/library/cc759226(v=ws.10).aspx)

[回線または電話にテレフォニーユーザーを割り当てる](https://technet.microsoft.com/library/cc736875(v=ws.10).aspx)

