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
ms.openlocfilehash: 0e453ef94aedb8920c0310123ff6033fafbaddab
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958624"
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
|/x|接続指向のコールバックを使用することに大量のトラフィックのネットワーク パケット損失が多いを指定します。 このパラメーターを省略すると、コネクションレス型コールバックが使用されます。|
|/c|必須。 クライアントのセットアップを指定します。|
|\<Server1>|必須。 クライアントで使用される TAPI サービス プロバイダーのあるリモート サーバーの名前を指定します。 クライアントはサービス プロバイダーの回線や電話を使用します。 クライアントは、サーバーと同じドメインまたはサーバーを含むドメインと双方向の信頼関係があるドメインにする必要があります。|
|\<Server2>…|その他のサーバーまたはこのクライアントに利用可能なサーバーを指定します。 サーバーの一覧を指定する場合は、スペースを使用して、サーバー名を区切ります。|
|/d|リモート サーバーの一覧をクリアします。 リモート サーバー上にある TAPI サービス プロバイダーを使用できなくなり、TAPI クライアントを無効にします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   この手順を実行するには、ローカル コンピューターの Administrators グループのメンバーであるか、適切な権限が委任されている必要があります。 コンピューターがドメインに追加されると、Domain Admins グループのメンバーは、この手順を実行できる場合があります。 セキュリティの点から、[**別のユーザーとして実行**] を使用してこの手順を実行することを検討してください。
-   TAPI が正しく機能するためには、実行する必要があります **tcmsetup** TAPI クライアントによって使用されるリモート サーバーを指定します。
-   クライアント ユーザーは、TAPI サーバー上、電話または回線を使用できるように、テレフォニー サーバーの管理者は、電話または回線にユーザーを割り当てる必要があります。
-   このコマンドによって作成されるテレフォニー サーバーの一覧には、クライアントで利用できるテレフォニー サーバーの既存の一覧が置き換えられます。 このコマンドを使用、既存のリストに追加することはできません。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[コマンド シェルの概要](/previous-versions/windows/it-pro/windows-server-2003/cc737438(v=ws.10))

[クライアント コンピューター上のテレフォニー サーバーを指定します。](/previous-versions/windows/it-pro/windows-server-2003/cc759226(v=ws.10))

[回線または電話に対してテレフォニー ユーザーを割り当てる](/previous-versions/windows/it-pro/windows-server-2003/cc736875(v=ws.10))
