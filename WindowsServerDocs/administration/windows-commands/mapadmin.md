---
title: mapadmin
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ad9f55ba130014227326f4abe8540c78755f6c5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437372"
---
# <a name="mapadmin"></a>mapadmin



使用することができます**Mapadmin** Microsoft Services for Network File System 用のユーザー名マッピングを管理します。

## <a name="syntax"></a>構文
```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <WindowsUser> -uu <UNIXUser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <WindowsGroup> -ug <UNIXGroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <WindowsUser> [-uu <UNIXUser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <WindowsGroup> [-ug <UNIXGroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename> 
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <WindowsDomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <WindowsDomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

## <a name="description"></a>説明
**Mapadmin**コマンド ライン ユーティリティが、管理ユーザー名マッピング Microsoft Services for Network File System を実行しているローカルまたはリモート コンピューターにします。 管理者の資格情報がないアカウントでログオンしている場合は、ユーザー名とは、アカウントのパスワードを指定できます。

特定のコマンド引数に加えて、 **mapadmin**次のオプションと引数を受け取ります。

&lt;コンピューター&gt;を管理するユーザー名マッピング サービスを実行しているリモート コンピューターを指定します。 Windows インターネット ネーム サービス (WINS) または、ドメイン ネーム システム (DNS) 名を使用してコンピューターを指定したり、インターネット プロトコル (IP) によって対処できます。

-u&lt;ユーザー&gt;資格情報を使用するユーザーのユーザー名を指定します。 フォームのユーザー名にドメイン名を追加する必要があります<em>ドメイン</em> **\\** <em>ユーザー名</em>します。

-p&lt;パスワード&gt;ユーザーのパスワードを指定します。 指定した場合、 **-u**オプションは、省略、 **-p**オプション、ユーザーのパスワードを求められます。
特定のアクションを**mapadmin**実行を指定するコマンド引数によって異なります。

## <a name="parameters"></a>パラメーター
### <a name="start"></a>start
ユーザー名マッピング サービスを開始します。

### <a name="stop"></a>stop
ユーザー名マッピング サービスを停止します。

### <a name="config"></a>構成
ユーザー名マッピングの全般設定を指定します。 このコマンドの引数では、次のオプション: **-r &lt;dddd&gt;:&lt;hh&gt;:&lt;mm&gt;**  -の更新間隔を指定します日、時間、および分単位では、Windows および NIS データベースから更新しています。 間隔の最小値は、5 分です。
**-i {[はい] | ありません}** -単純なマッピングをオンにする ( **[はい]** ) かオフ (**ありません**)。 既定では、単純なマッピングはでは。
**追加**-新しいユーザーまたはグループのマッピングを作成します。 次のオプションは、このコマンドの引数で使用できます。

|オプション|定義|
|-----|-------|
|-wu &lt;name&gt;|新しいマッピングが作成されている Windows ユーザーの名前を指定します。|
|-uu &lt;name&gt;|新しいマッピングが作成される対象の UNIX ユーザーの名前を指定します。|
|-wg &lt;group&gt;|新しいマッピングが作成されている Windows グループの名前を指定します。|
|-ug&lt;グループ&gt;|新しいマッピングが作成される対象の UNIX グループの名前を指定します。|
|-setprimary|新しいマッピングがプライマリのマッピングであることを指定します。|

**setprimary** -マッピングが複数のマッピングを使用して、プライマリの UNIX のユーザーまたはグループのマッピングを指定します。 次のオプションは、このコマンドの引数で使用できます。

|オプション|定義|
|-----|-------|
|-wu &lt;name&gt;|プライマリのマッピングの Windows ユーザーを指定します。 ユーザーの 1 つ以上のマッピングが存在する場合は、使用、 **- uu**プライマリのマッピングを指定するオプション。|
|-uu &lt;name&gt;|プライマリのマッピングの UNIX ユーザーを指定します。|
|-wg &lt;group&gt;|プライマリのマッピングの Windows グループを指定します。 グループの 1 つ以上のマッピングが存在する場合は、使用、 **- ug**プライマリのマッピングを指定するオプション。|
|-ug&lt;グループ&gt;|プライマリのマッピングの UNIX グループを指定します。|

**削除**-ユーザーまたはグループのマッピングを削除します。 このコマンドの引数は次のオプションです。

|オプション|定義|
|-----|-------|
|-wu &lt;user&gt;|このマッピングは削除、として指定された Windows ユーザー &lt; *WindowsDomain&gt;\\&lt;ユーザー名&gt;* します。 いずれかを指定する必要があります、 **-wu**または **- uu**オプション、またはその両方です。 両方のオプションを指定する場合は、2 つのオプションで識別される特定のマッピングが削除されます。 のみを指定する場合、 **-wu**オプションの場合は、指定したユーザーが削除のすべてのマッピング。|
|-wg &lt;group&gt;|このマッピングは削除、として指定された Windows グループ&lt;WindowsDomain&gt;\\&lt;groupname&gt;します。 いずれかを指定する必要があります、 **- wg**または **- ug**オプション、またはその両方です。 両方のオプションを指定する場合は、2 つのオプションで識別される特定のマッピングが削除されます。 のみを指定する場合、 **- wg**オプションの場合は、指定したグループは削除のすべてのマッピング。|
|-uu &lt;user&gt;|ユーザー マッピングは削除、として指定した UNIX ユーザー&lt;ユーザー名&gt;します。 いずれかを指定する必要があります、 **-wu**または **- uu**オプション、またはその両方です。 両方のオプションを指定する場合は、2 つのオプションで識別される特定のマッピングが削除されます。 のみを指定する場合、 **- uu**オプションの場合は、指定したユーザーが削除のすべてのマッピング。|
|-ug&lt;グループ&gt;|このマッピングは削除、として指定する UNIX グループ&lt;groupname&gt;します。 いずれかを指定する必要があります、 **- wg**または **- ug**オプション、またはその両方です。 両方のオプションを指定する場合は、2 つのオプションで識別される特定のマッピングが削除されます。 のみを指定する場合、 **- ug**オプションの場合は、指定したグループは削除のすべてのマッピング。|

**リスト**-ユーザーとグループのマッピングに関する情報が表示されます。 次のオプションは、このコマンドの引数で使用できます。

|オプション|定義|
|-----|-------|
|-すべて|ユーザーとグループの単純かつ高度なマッピングを一覧表示します。|
|-シンプル|すべての単純なマップされたユーザーとグループを一覧表示します。|
|-高度な|すべての高度なマップされたユーザーとグループを一覧表示します。 マップは、評価される順序で表示されます。 プライマリ マップ、アスタリスク (*) は、セカンダリのマップは、キャレット (^) でマークされた後に最初に、表示されます。|
|-wu &lt;name&gt;|指定された Windows ユーザー マッピングを一覧表示します。|
|-wg &lt;group&gt;|Windows グループのマッピングを一覧表示します。|
|-uu &lt;name&gt;|UNIX ユーザーのマッピングを一覧表示します。|
|-ug&lt;グループ&gt;|UNIX グループのマッピングを一覧表示します。|

**バックアップ**- 保存ユーザー名マッピングの構成とデータで指定されたファイルをマッピングする&lt;filename&gt;します。
**復元**-構成およびマッピングのデータをファイルからのデータに置き換えます (で指定された&lt;filename&gt;) を使用して作成された、**バックアップ**コマンド引数。
**adddomainmap** -Windows ドメインと NIS のドメインまたはパスワードとグループ ファイルの間の単純なマップを追加します。 このコマンドの引数は次のオプションです。

|オプション|定義|
|-----|-------|
|-d &lt;WindowsDomain&gt;|マップされることを Windows ドメインを指定します。|
|-y &lt;NISdomain&gt;|マップを NIS ドメインを指定します。&lt;br/&gt;&lt;br/&gt; **-n** &lt;nis サーバー&gt; NIS サーバーで指定された NIS ドメインを指定します、 **-y**オプション。|
|-f&lt;パス&gt;|マップするパスワードとグループ ファイルを含むディレクトリの完全修飾パスを指定します。 ファイルは、管理されているコンピューターに存在する必要があり、使用することはできません**mapadmin**パスワードとグループ ファイルに基づいてマップを設定するリモート コンピューターを管理します。|

**removedomainmap** -Windows ドメインと NIS ドメインの間の単純なマップを削除します。 次のオプションと引数は、このコマンドの引数です。

|オプション|定義|
|-----|-------|
|-d &lt;WindowsDomain&gt;|削除するマップの Windows ドメインを指定します。|
|-y &lt;NISdomain&gt;|削除するマップの NIS ドメインを指定します。|
|-すべて|Windows および NIS ドメインの間のすべての単純なマップが削除されることを指定します。 これは、Windows ドメイン、パスワード、およびグループのファイル間の任意の単純なマップも削除されます。|

**listdomainmaps** -NIS ドメインまたはパスワードとグループのファイルにマップされている Windows ドメインを一覧表示します。

## <a name="notes"></a>メモ
-   コマンドの引数を指定しない場合**mapadmin**ユーザー名マッピングの現在の設定が表示されます。
-   ユーザーまたはグループ名を指定するすべてのオプションについては、次の形式を使用できます。
-   Windows ユーザーは、フォームを使用して&lt;ドメイン&gt;\\&lt;ユーザー名&gt;、 \\ \\&lt;コンピューター&gt;\\&lt;ユーザー名前&gt;、 \\&lt;コンピューター&gt;\\&lt;ユーザー名&gt;、または&lt;コンピューター&gt;\\&lt;ユーザー名&gt;
-   Windows グループの場合は、フォームを使用して&lt;ドメイン&gt;\\&lt;&lt;groupname&gt;&gt;、 \\ \\&lt;コンピューター&gt;\\ &lt; &lt;groupname&gt;&gt;、 \\&lt;コンピューター&gt;\\&lt;&lt;groupname&gt; &gt;、または&lt;コンピューター&gt;\\&lt;&lt;groupname&gt;&gt;
-   UNIX ユーザーの場合は、フォームを使用して&lt;NISdomain&gt;\\&lt;ユーザー名&gt;、&lt;ユーザー名&gt;@&lt;NISdomain&gt;、ユーザー&lt;名前&gt;@PCNFS、または PCNFS\\&lt;ユーザー名&gt;
-   UNIX グループの場合は、フォームを使用して&lt;NISdomain&gt;\\&lt;groupname&gt;、 &lt;groupname&gt;@&lt;NISdomain&gt;、 &lt;groupname&gt;@PCNFS、または PCNFS\\&lt;groupname&gt;

## <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)
