---
title: waitfor
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: aecea0ad19ee42e61396eb8b8ccd579b9ce2057b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362604"
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

|       パラメーター       |                                                                                         説明                                                                                          |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s \<Computer >     | 名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。 このパラメーターは、コマンドで指定されたすべてのファイルとフォルダーに適用されます。 |
| /u [\<Domain > \] @ no__t |                              指定したユーザー アカウントの資格情報を使用してスクリプトを実行します。 既定では、 **waitfor** 現在のユーザーの資格情報を使用します。                               |
|   /p [\<Password >]    |                                                    指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                     |
|          /si          |                                                                        ネットワーク経由で指定されたシグナルを送信します。                                                                        |
|     /t \<Timeout >     |                                              シグナルを待機する秒数を指定します。 既定では、 **waitfor** が無制限に待機します。                                               |
|     \<SignalName >     |                                                信号を指定する **waitfor** まで待機するか、または送信します。 *信号名* 小文字は区別されません。                                                 |
|          /?           |                                                                             コマンド プロンプトにヘルプを表示します。                                                                             |

## <a name="remarks"></a>コメント

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

[コマンド ライン構文の記号](command-line-syntax-key.md)