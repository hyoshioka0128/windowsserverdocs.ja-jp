---
title: gpfixup
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e32427369f1664476c81a81353ae8869ec0c2ff3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375670"
---
# <a name="gpfixup"></a>gpfixup



ドメイン名の変更操作後にグループポリシーオブジェクトおよびグループポリシーリンク内のドメイン名の依存関係を修正します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLATNAME> /newnb:<NEWFLATNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWORD>|*}]] [/?]
```

### <a name="parameters"></a>パラメーター

|       パラメーター       |                                                                                                                                                                                                                               説明                                                                                                                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /v           |                                                                                                                                                      詳細なステータスメッセージを表示します。</br>このパラメーターを使用しない場合は、エラーメッセージまたは**成功**または**失敗**の概要ステータスメッセージのみが表示されます。                                                                                                                                                       |
| /olddns: \<OLDDNSNAME > |                                                                                                           ドメインの名前変更操作によってドメインの DNS 名が変更された場合に *@no__t 1OLDDNSNAME >* として名前が変更されたドメインの古い DNS 名を指定します。 このパラメーターは、 **/newdns**パラメーターを使用して新しいドメイン dns 名を指定する場合にのみ使用できます。                                                                                                            |
| /newdns: \<NEWDNSNAME > |                                                                                                          ドメインの名前変更操作によってドメインの DNS 名が変更された場合に *@no__t 1NEWDNSNAME >* として名前が変更されたドメインの新しい dns 名を指定します。 このパラメーターは、古いドメイン DNS 名を指定するために、 **/olddns**パラメーターも使用する場合にのみ使用できます。                                                                                                           |
| /oldnb: \<OLDFLATNAME > |                                                                                                        ドメインの名前変更操作によってドメインの NetBIOS 名が変更された場合に *@no__t 1OLDFLATNAME >* として名前が変更されたドメインの古い NetBIOS 名を指定します。 このパラメーターは、 **/newnb**パラメーターを使用して新しいドメイン NetBIOS 名を指定する場合にのみ使用できます。                                                                                                        |
| /newnb: \<NEWFLATNAME > |                                                                                                       ドメインの名前変更操作によってドメインの NetBIOS 名が変更された場合に *@no__t 1NEWFLATNAME >* として名前が変更されたドメインの新しい netbios 名を指定します。 このパラメーターは、 **/oldnb**パラメーターを使用して古いドメイン NetBIOS 名を指定する場合にのみ使用できます。                                                                                                       |
|     /dc: \<DCNAME >     | *@No__t-1DCNAME >* (DNS 名または NetBIOS 名) という名前のドメインコントローラーに接続します。 *1DCNAME >* は、次のいずれかの方法で示されているように、ドメインディレクトリパーティションの書き込み可能なレプリカをホストする必要があります。 @no__t</br>-DNS 名 *@no__t 1NEWDNSNAME >* には、 **/dns dns**を使用します。</br>-NetBIOS 名 *@no__t 1NEWFLATNAME >* には、 **/newnb**を使用します。</br>このパラメーターが使用されていない場合は、 *\<NEWDNSNAME >* または *\<NEWFLATNAME >* によって示される、名前が変更されたドメイン内の任意のドメインコントローラーに接続します。 |
|        /sionly        |                                                                                                                           は、管理されているソフトウェアのインストール (グループポリシーのソフトウェアインストール拡張機能) に関連するグループポリシー修正プログラムのみを実行します。 Gpo のグループポリシーリンクと SYSVOL パスを修正する操作をスキップします。                                                                                                                           |
|   /user: \<USERNAME >   |                                                                                                                                   このコマンドをユーザーのセキュリティコンテキストで実行 *\< ユーザー名 >* です。 *\<username >* は domain\user という形式になっています。</br>このパラメーターが使用されていない場合、はログインしているユーザーとしてこのコマンドを実行します。                                                                                                                                    |
|   /pwd: {\<PASSWORD >   |                                                                                                                                                                                                                                   \*}                                                                                                                                                                                                                                   |
|          /?           |                                                                                                                                                                                                                  コマンド プロンプトでヘルプを表示します。                                                                                                                                                                                                                   |

## <a name="remarks"></a>コメント

-   **Gpfixup**コマンドは、server Core インストールを除き、windows Server 2008 R2 および windows server 2008 で使用できます。
-   グループポリシー管理コンソール (GPMC) は Windows Server 2008 R2 および Windows Server 2008 と共に配布されますが、サーバーマネージャーを通じてグループポリシー管理を機能としてインストールする必要があります。

## <a name="BKMK_Examples"></a>例

この例では、DNS 名を**MyOldDnsName**から**MyNewDnsName**に、NetBIOS 名を**MyOldNetBIOSName**から**MyNewNetBIOSName**に変更したドメインの名前変更操作を既に実行していることを前提としています。 この例では、 **gpfixup**コマンドを使用して、gpo とリンクに埋め込まれている古いドメイン名を更新することによって、 **Mydcdnsname 名**という名前のドメインコントローラーに接続し、gpo とグループポリシーリンクを修復します。 状態およびエラー出力は、 **gpfixup .log**という名前のファイルに保存されます。
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
この例は前の例と同じですが、ドメインの名前変更操作中にドメインの NetBIOS 名が変更されていないことを前提としています。
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

#### <a name="additional-references"></a>その他の参照情報

-   [Active Directory ドメインの名前変更の管理](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [グループポリシー TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)