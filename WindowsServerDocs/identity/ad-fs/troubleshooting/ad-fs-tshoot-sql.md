---
title: AD FS のトラブルシューティング - SQL 接続
description: このドキュメントは、AD FS のさまざまな側面をトラブルシューティングする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a4b7a568200bee7c2696c57f1dd964dd4e84ec21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820263"
---
# <a name="ad-fs-troubleshooting---sql-connectivity"></a>AD FS のトラブルシューティング - SQL 接続
AD FS では、リモートの SQL Server の AD FS ファームのデータを使用する機能を提供します。  ファーム内の AD FS サーバーは、バックエンド SQL サーバーと通信できない場合、問題が表示されます。  次のドキュメントでは、バックエンド サーバーとの通信をテストするいくつかの基本的な手順を説明します。

## <a name="acquire-the-sql-database-connection-string"></a>SQL データベースの接続文字列を取得します。
SQL 接続を確認するときにテストするには、まずは、AD FS には、正しい SQL 接続情報が含まれている場合は。  これ行う PowerShell を使用します。

### <a name="to-acquire-the-sql-connection-string"></a>SQL 接続文字列を取得するには
1.  開いている Windows PowerShell
2. 次を入力します:`$adfs = gwmi -Namespace root/ADFS -Class SecurityTokenService`し、Enter キー
3. 次を入力します:`$adfs.ConfigurationDatabaseConnectionString`し、enter キーを押します。
4. 接続文字列の情報が表示されます。
![](media/ad-fs-tshoot-sql/sql2.png)

## <a name="create-a-universal-data-link-udl-file-to-test-connectivity"></a>接続をテストする Universal Data Link (UDL) ファイルを作成します。
ユニバーサル データ リンク ファイルまたは UDL ファイルを含むテキスト ファイルでは基本的には、データベース接続文字列。  上で取得した情報を使用して SQL server が接続に応答しているかどうかをテストできます。

### <a name="to-create-a-udl-file-to-test-connectivity"></a>接続をテストする udl ファイルを作成するには

1. メモ帳を開き、test.udl としてファイルを保存します。  いることを確認します**すべてのファイル**のドロップダウン リストから選択した**型として保存**します。
2. Test.udl をダブルクリックします
3. 次の情報を入力: をします。 **選択するか、サーバー名を入力します。** B 上の接続文字列からのデータ ソースを使用します。 **サーバーにログオンする情報を入力します。** AD FS サービス アカウントまたはリモートでログオンする権限を持つアカウントを使用します。  アカウントが統合された windows アカウントの使用の場合、それ以外の場合の認証は、ユーザー名とパスワードを入力します。
    c. **サーバー上のデータベースを選択します。** 上記の文字列からは、初期カタログを使用します。  以下に例を示します。AdfsConfigurationV3 します。
   ![[接続テスト]](media/ad-fs-tshoot-sql/sql4.png)
1. クリックして**接続をテストする**します。</br>
![成功](media/ad-fs-tshoot-sql/sql3.png)

## <a name="use-sql-server-management-studio-to-test-connectivity"></a>SQL Server Management Studio を使用して接続をテストするには
できます[ダウンロード](https://go.microsoft.com/fwlink/?linkid=864329)し、データベース接続をテストする SSMS をインストールします。

###<a name="to-test-connectivity-with-ssms"></a>SSMS を使用した接続をテストするには
1. ダウンロードし、SQL Server Management Studio をインストールします。
![インストール](media/ad-fs-tshoot-sql/sql5.png)
1. SSMS を開き、サーバー名を入力します。  上記のデータ ソース。
2. AD FS サービス アカウントまたはリモートでログオンする権限を持つアカウントを使用します。  アカウントが統合された windows アカウントの使用の場合、それ以外の場合の認証は、ユーザー名とパスワードを入力します。
![Connect](media/ad-fs-tshoot-sql/sql6.png)
1. 左側にある設定が表示されます。  データベースを展開し、AD FS データベースを表示することを確認します。
![AD FS データベース](media/ad-fs-tshoot-sql/sql7.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)