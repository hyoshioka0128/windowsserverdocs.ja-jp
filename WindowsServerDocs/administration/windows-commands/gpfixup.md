---
title: gpfixup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: efb30e243d9c165fdcf13943225eb90d38235070
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438214"
---
# <a name="gpfixup"></a>gpfixup



ドメイン操作の名前を変更した後は、グループ ポリシー オブジェクトとグループ ポリシーのリンクのドメイン名の依存関係を修正します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

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
|          /v           |                                                                                                                                                      詳細なステータス メッセージが表示されます。</br>このパラメーターを使用しない場合は、エラー メッセージのみまたは概要の状態メッセージを**成功**または**エラー**が表示されます。                                                                                                                                                       |
| /olddns:\<OLDDNSNAME > |                                                                                                           名前が変更されたドメインの古い DNS 名を指定します *\<OLDDNSNAME >* ドメインの名前の変更操作が、ドメインの DNS 名に変更されたとき。 このパラメーターを使用するには、使用する場合にのみ、 **/newdns**新しいドメインの DNS 名を指定するパラメーター。                                                                                                            |
| /newdns:\<NEWDNSNAME > |                                                                                                          名前が変更されたドメインの新しい DNS 名を指定します *\<NEWDNSNAME >* ドメインの名前の変更操作が、ドメインの DNS 名に変更されたとき。 このパラメーターを使用するには、使用する場合にのみ、 **/olddns**古いドメインの DNS 名を指定するパラメーター。                                                                                                           |
| /oldnb:\<OLDFLATNAME> |                                                                                                        名前が変更されたドメインの古い NetBIOS 名を指定します *\<OLDFLATNAME >* ドメインの名前の変更操作で、ドメインの NetBIOS 名が変更されたとき。 このパラメーターを使用するには、使用する場合にのみ、 **/newnb**パラメーターを新しいドメインの NetBIOS 名を指定します。                                                                                                        |
| /newnb:\<NEWFLATNAME > |                                                                                                       名前が変更されたドメインの新しい NetBIOS 名を指定します *\<NEWFLATNAME >* ドメインの名前の変更操作で、ドメインの NetBIOS 名が変更されたとき。 このパラメーターを使用するには、使用する場合にのみ、 **/oldnb**古いドメイン NetBIOS 名を指定するパラメーター。                                                                                                       |
|     /dc:\<DCNAME>     | という名前のドメイン コント ローラーに接続する *\<DCNAME >* (DNS 名または NetBIOS 名)。 *\<DCNAME >* 次のいずれかで示されている、ドメイン ディレクトリ パーティションの書き込み可能なレプリカをホストする必要があります。</br>DNS 名 *\<NEWDNSNAME >* を使用して **/newdns**</br>-NetBIOS 名 *\<NEWFLATNAME >* を使用して **/newnb**</br>このパラメーターを使用しない場合は、によって示される名前が変更されたドメイン内の任意のドメイン コント ローラーに接続 *\<NEWDNSNAME >* または *\<NEWFLATNAME >* します。 |
|        /sionly        |                                                                                                                           管理されているソフトウェアのインストール (グループ ポリシーのソフトウェアのインストールの拡張機能) に関連するグループ ポリシー修正プログラムのみを実行します。 Gpo のグループ ポリシーのリンクと SYSVOL のパスを修正するアクションをスキップします。                                                                                                                           |
|   /user:\<ユーザー名 >   |                                                                                                                                   ユーザーのセキュリティ コンテキストでこのコマンドを実行 *\<ユーザー名 >* ここで、 *\<ユーザー名 >* 形式 domain \user にします。</br>このパラメーターを使用しない場合は、ログインしているユーザーとしてこのコマンドを実行します。                                                                                                                                    |
|   /pwd: {\<パスワード >   |                                                                                                                                                                                                                                   \*}                                                                                                                                                                                                                                   |
|          /?           |                                                                                                                                                                                                                  コマンド プロンプトでヘルプを表示します。                                                                                                                                                                                                                   |

## <a name="remarks"></a>注釈

-   **Gpfixup**コマンドには、Windows Server 2008 R2 および Windows Server 2008 では、Server Core インストールする場合は除きます。
-   グループ ポリシー管理コンソール (GPMC) は、Windows Server 2008 R2 および Windows Server 2008 と共に配布は、サーバー マネージャーから機能としてグループ ポリシーの管理をインストールする必要があります。

## <a name="BKMK_Examples"></a>例

この例から DNS 名を変更したドメイン名の変更操作が既に実行**MyOldDnsName**に**MyNewDnsName**、および NetBIOS 名から**MyOldNetBIOSName**に**MyNewNetBIOSName**します。 この例では使用して、 **gpfixup**という名前のドメイン コント ローラーに接続するためのコマンド**MyDcDnsName** Gpo およびグループ ポリシーの修復と Gpo とリンクに埋め込まれている古いドメイン名を更新することによってリンクします。 状態とエラー出力がという名前のファイルに保存する**gpfixup.log**します。
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
この例は前と同じで、ドメインの NetBIOS 名、ドメインの中に変更しないことを前提としていますが、操作の名前を変更します。
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

#### <a name="additional-references"></a>その他の参照情報

-   [Active Directory ドメイン名の変更を管理します。](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [グループ ポリシーの TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)