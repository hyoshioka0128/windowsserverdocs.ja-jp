---
title: waitfor
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a48ef70d-4d28-4035-b6b0-7d7b46ac2157
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1c4a91dd3822cf4d8dd904f473f146a2f0ee54c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840163"
---
# <a name="waitfor"></a>waitfor



送信またはシステムでのシグナルを待機します。 **Waitfor** をネットワーク経由でコンピューターを同期するために使用します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
waitfor [/s <Computer> [/u [<Domain>\]<User> [/p [<Password>]]]] /si <SignalName>
waitfor [/t <Timeout>] <SignalName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<コンピューター >|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。 このパラメーターは、すべてのファイルと、コマンドで指定したフォルダーに適用されます。|
|/u [\<ドメイン >\]<User>|指定したユーザー アカウントの資格情報を使用してスクリプトを実行します。 既定では、 **waitfor** 現在のユーザーの資格情報を使用します。|
|/p [\<パスワード >]|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/si|ネットワーク経由で指定されたシグナルを送信します。|
|/t\<タイムアウト >|シグナルを待機する秒数を指定します。 既定では、 **waitfor** が無制限に待機します。|
|\<SignalName>|信号を指定する **waitfor** まで待機するか、または送信します。 *信号名* 小文字は区別されません。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   シグナル名には、225 文字を超えることはできません。 有効な文字には、a ~ z、A ~ Z、0 ~ 9、および拡張文字セット (128 ~ 255) ASCII が含まれます。
-   使用しない場合 **/s**, 、信号は、ドメイン内のすべてのシステムにブロードキャストされます。 使用する場合 **/s**, 、信号が、指定したシステムにのみ送信します。
-   複数のインスタンスを実行する **waitfor** 1 台のコンピューターではの各インスタンスで **waitfor** 異なるシグナルを待機する必要があります。 1 つだけ **waitfor** 、特定のコンピューター上で指定されたシグナルを待機できます。
-   使用して、信号を手動でアクティブ、 **/si** コマンド ライン オプションです。
-   **Waitfor** に Windows XP と Windows Server 2003 オペレーティング システムを実行しているサーバーのみで実行されますが、Windows オペレーティング システムを実行しているコンピューターの信号を送信することができます。
-   のみ、コンピューターは、信号を送信するコンピューターと同じドメイン内にある場合、シグナルを受信します。
-   使用する **waitfor** ソフトウェア ビルドをテストする場合。 コンパイルを行うコンピューターが実行されている複数のコンピューターに信号を送信するなど **waitfor** コンパイルが正常に完了後します。 信号の要求を受信したバッチ ファイルを含む **waitfor** コンピューターがすぐにソフトウェアのインストールやコンパイル済みのビルドでテストを実行するように指定できます。

## <a name="BKMK_examples"></a>例

"\Build007"信号を受信するまで待機するには、次のように入力します。
```
waitfor espresso\build007
```
既定では、 **waitfor** シグナルを無期限に待機します。

タイムアウトするまでに受信"espresso\compile007"信号を 10 秒間待機するには、次のように入力します。
```
waitfor /t 10 espresso\build007
```
"\Build007"信号を手動でアクティブ化には、次のように入力します。
```
waitfor /si espresso\build007
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)