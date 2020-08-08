---
title: AD FS のトラブルシューティング-SQL 接続
description: このドキュメントでは、AD FS のさまざまな側面をトラブルシューティングする方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2017
ms.topic: article
ms.openlocfilehash: 2fb32d5b553b4d248c718fac766a83daa5dfedb2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964819"
---
# <a name="ad-fs-troubleshooting---sql-connectivity"></a>AD FS のトラブルシューティング-SQL 接続
AD FS には、AD FS ファームデータに対してリモート SQL Server を使用する機能が用意されています。  ファーム内の AD FS サーバーがバックエンド SQL サーバーと通信できない場合は、問題が発生します。  次のドキュメントでは、バックエンドサーバーとの通信をテストする基本的な手順について説明します。

## <a name="acquire-the-sql-database-connection-string"></a>SQL database の接続文字列を取得する
SQL 接続をチェックするときに最初にテストするのは、AD FS に正しい SQL 接続情報があるかどうかです。  これは、PowerShell を使用して行うことができます。

### <a name="to-acquire-the-sql-connection-string"></a>SQL 接続文字列を取得するには
1.  Windows PowerShell を開く
2. 次のように入力し、 `$adfs = gwmi -Namespace root/ADFS -Class SecurityTokenService` Enter キーを押します。
3. 次のように入力して、 `$adfs.ConfigurationDatabaseConnectionString` enter キーを押します。
4. 接続文字列の情報が表示されます。

![コマンドを実行する PowerShell コマンド画面](media/ad-fs-tshoot-sql/sql2.png)

## <a name="create-a-universal-data-link-udl-file-to-test-connectivity"></a>接続をテストするためのユニバーサルデータリンク (UDL) ファイルを作成する
ユニバーサルデータリンクファイルまたは UDL ファイルは、基本的にはデータベース接続文字列を含むテキストファイルです。  上記で取得した情報を使用して、SQL server が接続に応答しているかどうかをテストできます。

### <a name="to-create-a-udl-file-to-test-connectivity"></a>接続をテストするための udl ファイルを作成するには

1. メモ帳を開き、ファイルを test .udl として保存します。  [**種類] として [保存**] で、**すべてのファイル**が選択されていることを確認します。
2. [.Udl] をダブルクリックします。
3. 次の情報を入力します。 a. **サーバー名の選択または入力:** B の上の接続文字列のデータソースを使用します。 **サーバーにログオンするための情報を入力してください:** AD FS サービスアカウント、またはリモートでログオンするためのアクセス許可を持つアカウントを使用します。  アカウントが windows アカウントの場合は、統合認証を使用します。それ以外の場合は、ユーザー名とパスワードを入力します。
    c. **サーバー上のデータベースを選択します。** 上記の文字列の初期カタログを使用します。  例: AdfsConfigurationV3。
   ![[接続テスト]](media/ad-fs-tshoot-sql/sql4.png)
1. **[接続テスト]** をクリックします。</br>
![Success](media/ad-fs-tshoot-sql/sql3.png)

## <a name="use-sql-server-management-studio-to-test-connectivity"></a>SQL Server Management Studio を使用して接続をテストする
SSMS を[ダウンロード](https://go.microsoft.com/fwlink/?linkid=864329)してインストールし、データベース接続をテストすることもできます。

### <a name="to-test-connectivity-with-ssms"></a>SSMS を使用した接続をテストするには
1. SQL Server Management Studio をダウンロードしてインストールします。
![インストール](media/ad-fs-tshoot-sql/sql5.png)
1. SSMS を開き、サーバー名を入力します。  上記のデータソース。
2. AD FS サービスアカウント、またはリモートでログオンするためのアクセス許可を持つアカウントを使用します。  アカウントが windows アカウントの場合は、統合認証を使用します。それ以外の場合は、ユーザー名とパスワードを入力します。
![接続する](media/ad-fs-tshoot-sql/sql6.png)
1. 左側に値が設定されていることがわかります。  [データベース] を展開し、AD FS データベースが表示されていることを確認します。
![AD FS データベース](media/ad-fs-tshoot-sql/sql7.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)