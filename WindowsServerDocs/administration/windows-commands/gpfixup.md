---
title: gpfixup
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6df3b2fabcbfad29576a8e8f48d6a1a87f0da2ce
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724960"
---
# <a name="gpfixup"></a>gpfixup



ドメイン名の変更操作後にグループポリシーオブジェクトおよびグループポリシーリンク内のドメイン名の依存関係を修正します。

## <a name="syntax"></a>構文

```
Gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLATNAME> /newnb:<NEWFLATNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWORD>|*}]] [/?]
```

#### <a name="parameters"></a>パラメーター

|       パラメーター       |                                                                                                                                                                                                                               [説明]                                                                                                                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /v           |                                                                                                                                                      詳細なステータスメッセージを表示します。</br>このパラメーターを使用しない場合は、エラーメッセージまたは**成功**または**失敗**の概要ステータスメッセージのみが表示されます。                                                                                                                                                       |
| /olddns:\<OLDDNSNAME> |                                                                                                           ドメインの名前変更操作によってドメインの dns 名が変更された場合に、名前が変更されたドメインの古い DNS 名を* \<OLDDNSNAME>* として指定します。 このパラメーターは、 **/newdns**パラメーターを使用して新しいドメイン dns 名を指定する場合にのみ使用できます。                                                                                                            |
| /newdns:\<NEWDNSNAME> |                                                                                                          ドメインの名前変更操作によってドメインの dns 名が変更された場合に、名前が変更されたドメインの新しい dns 名を* \<NEWDNSNAME>* として指定します。 このパラメーターは、古いドメイン DNS 名を指定するために、 **/olddns**パラメーターも使用する場合にのみ使用できます。                                                                                                           |
| /oldnb:\<OLDFLATNAME> |                                                                                                        ドメインの名前変更操作によってドメインの netbios 名が変更された場合に、名前が変更されたドメインの古い NetBIOS 名を* \<OLDFLATNAME>* として指定します。 このパラメーターは、 **/newnb**パラメーターを使用して新しいドメイン NetBIOS 名を指定する場合にのみ使用できます。                                                                                                        |
| /newnb:\<NEWFLATNAME> |                                                                                                       ドメインの名前変更操作によってドメインの netbios 名が変更された場合に、名前が変更されたドメインの新しい netbios 名を* \<NEWFLATNAME>* として指定します。 このパラメーターは、 **/oldnb**パラメーターを使用して古いドメイン NetBIOS 名を指定する場合にのみ使用できます。                                                                                                       |
|     /dc:\<DCNAME>     | * \<DCNAME>* という名前のドメインコントローラー (DNS 名または NetBIOS 名) に接続します。 DCNAME>は、次のいずれかの方法で示されているように、ドメインディレクトリパーティションの書き込み可能なレプリカをホストする必要があります。 * \<*</br>-Dns 名* \<NEWDNSNAME>* には、 **/dns dns**を使用します。</br>-NetBIOS 名* \<NEWFLATNAME*は、 **/newnb**を使用して>ます。</br>このパラメーターが使用されていない場合は、名前を変更したドメイン内の任意のドメインコントローラーに接続します。 * \<NEWDNSNAME>* または* \<NEWFLATNAME>* によって示されます。 |
|        /sionly        |                                                                                                                           は、管理されているソフトウェアのインストール (グループポリシーのソフトウェアインストール拡張機能) に関連するグループポリシー修正プログラムのみを実行します。 Gpo のグループポリシーリンクと SYSVOL パスを修正する操作をスキップします。                                                                                                                           |
|   /user:\<ユーザー名>   |                                                                                                                                   このコマンドは、ユーザー * \<のユーザー名>* のセキュリティコンテキストで実行されます。 * \<username>* は domain\user という形式になっています。</br>このパラメーターが使用されていない場合、はログインしているユーザーとしてこのコマンドを実行します。                                                                                                                                    |
|   /pwd: {\<パスワード>   |                                                                                                                                                                                                                                   \*}                                                                                                                                                                                                                                   |
|          /?           |                                                                                                                                                                                                                  コマンド プロンプトでヘルプを表示します。                                                                                                                                                                                                                   |

## <a name="remarks"></a>Remarks

-   **Gpfixup**コマンドは、server Core インストールを除き、windows Server 2008 R2 および windows server 2008 で使用できます。
-   グループポリシー管理コンソール (GPMC) は Windows Server 2008 R2 および Windows Server 2008 と共に配布されますが、サーバーマネージャーを通じてグループポリシー管理を機能としてインストールする必要があります。

## <a name="examples"></a>例

この例では、DNS 名を**MyOldDnsName**から**MyNewDnsName**に、NetBIOS 名を**MyOldNetBIOSName**から**MyNewNetBIOSName**に変更したドメインの名前変更操作を既に実行していることを前提としています。 この例では、 **gpfixup**コマンドを使用して、gpo とリンクに埋め込まれている古いドメイン名を更新することによって、 **Mydcdnsname 名**という名前のドメインコントローラーに接続し、gpo とグループポリシーリンクを修復します。 状態およびエラー出力は、 **gpfixup .log**という名前のファイルに保存されます。
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
この例は前の例と同じですが、ドメインの名前変更操作中にドメインの NetBIOS 名が変更されていないことを前提としています。
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>その他のリファレンス

-   [Active Directory ドメインの名前変更の管理](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [TechCenter のグループ ポリシー](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)