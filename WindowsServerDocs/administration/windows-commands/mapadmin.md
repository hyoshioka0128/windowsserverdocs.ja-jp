---
title: mapadmin
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fc4b76c1989298ea83c480b9c838ce0fc18fef5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373759"
---
# <a name="mapadmin"></a>mapadmin



**Mapadmin**を使用して、ネットワークファイルシステム用の Microsoft サービスのユーザー名マッピングを管理できます。

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
**Mapadmin**コマンドラインユーティリティは、ネットワークファイルシステム用に Microsoft サービスを実行しているローカルコンピューターまたはリモートコンピューター上でユーザー名マッピングを管理します。 管理者の資格情報がないアカウントでログオンしている場合は、を実行するアカウントのユーザー名とパスワードを指定できます。

**Mapadmin**は、特定のコマンド引数に加えて、次の引数とオプションを受け取ります。

&lt;computer @ no__t-1 は、管理するユーザー名マッピングサービスを実行しているリモートコンピューターを指定します。 Windows インターネットネームサービス (WINS) 名またはドメインネームシステム (DNS) 名またはインターネットプロトコル (IP) アドレスを使用して、コンピューターを指定できます。

-u &lt;user @ no__t-1 は、資格情報を使用するユーザーのユーザー名を指定します。 ドメイン **\\** <em>ユーザー名</em><em>の形式で</em>ドメイン名をユーザー名に追加することが必要になる場合があります。

-p &lt;password @ no__t-1 ユーザーのパスワードを指定します。 \- **U**オプションを指定しても **-p**オプションを省略した場合、ユーザーのパスワードの入力を求められます。
**Mapadmin**が実行する特定のアクションは、指定するコマンド引数によって異なります。

## <a name="parameters"></a>パラメーター
### <a name="start"></a>start
ユーザー名マッピングサービスを開始します。

### <a name="stop"></a>stop
ユーザー名マッピングサービスを停止します。

### <a name="config"></a>構成
ユーザー名マッピングの全般設定を指定します。 このコマンド引数では、次のオプションを使用できます。 **-r &lt;dddd @ no__t-2: &lt;hh @ no__t-4: &lt; mm @ no__t** -WINDOWS および NIS データベースから更新する更新間隔を日、時間、分単位で指定します。 最小間隔は5分です。
**-i {yes | no}** -単純なマッピングをオン (**はい**) またはオフ (**いいえ**) にします。 既定では、単純なマッピングはオンになっています。
**[追加]** : ユーザーまたはグループの新しいマッピングを作成します。 このコマンド引数では、次のオプションを使用できます。

|OPTION|定義|
|-----|-------|
|-wu &lt;name @ no__t-1|新しいマッピングを作成する Windows ユーザーの名前を指定します。|
|-uu &lt;name @ no__t-1|新しいマッピングを作成する UNIX ユーザーの名前を指定します。|
|-wg &lt;group @ no__t-1|新しいマッピングを作成する Windows グループの名前を指定します。|
|-ug &lt;group @ no__t-1|新しいマッピングを作成する UNIX グループの名前を指定します。|
|-setprimary|新しいマッピングがプライマリマッピングであることを指定します。|

**setprimary** -複数のマッピングを持つ UNIX ユーザーまたはグループのプライマリマッピングであるマッピングを指定します。 このコマンド引数では、次のオプションを使用できます。

|OPTION|定義|
|-----|-------|
|-wu &lt;name @ no__t-1|プライマリマッピングの Windows ユーザーを指定します。 ユーザーに対して複数のマッピングが存在する場合は、 **-uu**オプションを使用してプライマリマッピングを指定します。|
|-uu &lt;name @ no__t-1|プライマリマッピングの UNIX ユーザーを指定します。|
|-wg &lt;group @ no__t-1|プライマリマッピングの Windows グループを指定します。 グループに対して複数のマッピングが存在する場合は、 **-ug**オプションを使用してプライマリマッピングを指定します。|
|-ug &lt;group @ no__t-1|プライマリマッピングの UNIX グループを指定します。|

**削除**-ユーザーまたはグループのマッピングを削除します。 このコマンド引数には、次のオプションを使用できます。

|OPTION|定義|
|-----|-------|
|-wu &lt;user @ no__t-1|マッピングを削除する Windows ユーザーを &lt;*Windowsdomain @ no__t-2 @ no__t @ no__t-4User Name @ no__t-5*として指定します。 **-Wu**または **-uu**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Wu**オプションのみを指定すると、指定したユーザーのすべてのマッピングが削除されます。|
|-wg &lt;group @ no__t-1|マッピングを削除する対象の Windows グループ。 &lt;WindowsDomain @ no__t のように指定します。 @ no__t @ no__t-3groupname @ no__t-4 として指定します。 **-Wg**または **-ug**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Wg**オプションのみを指定すると、指定したグループのすべてのマッピングが削除されます。|
|-uu &lt;user @ no__t-1|@No__t-0User Name @ no__t-1 として指定されたマッピングを削除する UNIX ユーザー。 **-Wu**または **-uu**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Uu**オプションのみを指定すると、指定したユーザーのすべてのマッピングが削除されます。|
|-ug &lt;group @ no__t-1|マッピングが削除される UNIX グループ。 &lt;groupname @ no__t-1 として指定します。 **-Wg**または **-ug**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Ug**オプションのみを指定すると、指定したグループのすべてのマッピングが削除されます。|

**リスト**-ユーザーとグループのマッピングに関する情報を表示します。 このコマンド引数では、次のオプションを使用できます。

|OPTION|定義|
|-----|-------|
|-すべて|ユーザーとグループの単純なマッピングと高度なマッピングの両方を一覧表示します。|
|-シンプル|すべての単純なマップされたユーザーとグループを一覧表示します。|
|-詳細設定|すべての高度なマップされたユーザーとグループを一覧表示します。 マップは、評価される順序で一覧表示されます。 アスタリスク (*) が付いたプライマリマップが最初に一覧表示され、次にセカンダリマップがカラット (^) でマークされます。|
|-wu &lt;name @ no__t-1|指定された Windows ユーザーのマッピングを一覧表示します。|
|-wg &lt;group @ no__t-1|Windows グループのマッピングを一覧表示します。|
|-uu &lt;name @ no__t-1|UNIX ユーザーのマッピングを一覧表示します。|
|-ug &lt;group @ no__t-1|UNIX グループのマッピングを一覧表示します。|

**バックアップ**-&lt;filename @ no__t-2 で指定したファイルにユーザー名マッピングの構成とマッピングデータを保存します。
**復元**- **backup**コマンドの引数を使用して作成されたファイル (&lt;filename @ no__t-2 で指定) のデータと構成およびマッピングデータを置き換えます。
**adddomainmap** -Windows ドメインと NIS ドメイン、またはパスワードとグループファイルの間に単純なマップを追加します。 このコマンド引数には、次のオプションを使用できます。

|OPTION|定義|
|-----|-------|
|-d &lt;WindowsDomain @ no__t-1|マップする Windows ドメインを指定します。|
|-y &lt;Nis ドメイン @ no__t-1|マップする NIS ドメインを指定します。 &lt;br/&gt; @ no__t-2br/&gt; **-n** &lt;nis サーバー @ no__t-6 **-y**オプションで指定された nis ドメインの Nis サーバーを指定します。|
|-f &lt;path @ no__t-1|マップするパスワードおよびグループファイルを含むディレクトリの完全修飾パスを指定します。 ファイルは、管理されているコンピューターに配置する必要があります。 **mapadmin**を使用してリモートコンピューターを管理し、パスワードおよびグループファイルに基づいてマップを設定することはできません。|

**removedomainmap** -Windows ドメインと NIS ドメインとの間の単純なマップを削除します。 このコマンド引数には、次のオプションと引数を使用できます。

|OPTION|定義|
|-----|-------|
|-d &lt;WindowsDomain @ no__t-1|削除するマップの Windows ドメインを指定します。|
|-y &lt;Nis ドメイン @ no__t-1|削除するマップの NIS ドメインを指定します。|
|-すべて|Windows および NIS ドメイン間のすべての単純なマップを削除することを指定します。 これにより、Windows ドメインとパスワードおよびグループファイル間の単純なマップも削除されます。|

**listdomainmaps** -NIS ドメイン、パスワード、およびグループファイルにマップされている Windows ドメインを一覧表示します。

## <a name="notes"></a>メモ
-   コマンド引数を指定しない場合、 **mapadmin**では、ユーザー名マッピングの現在の設定が表示されます。
-   ユーザー名またはグループ名を指定するすべてのオプションについて、次の形式を使用できます。
-   Windows ユーザーの場合は、&lt;domain @ no__t-1 @ no__t @ no__t @ no__t-4 の形式を使用します。 \\ @ no__t @ no__t-7computer @ no__t-8 @ no__t-9 @ no__t-10user name @ no__t-11、&gt;2 @ no__t-13computer @ no__t-14 @ no__t-15 @ no__t-16user name @ no__t-17、または 8computer @ no__t-20 @ no__t ユーザー名 @ no__t-22
-   Windows グループの場合は、&lt;domain @ no__t @ no__t @ no__t @ no__t @ no__t-5 @-6 の形式を使用します。 \\ @ no__t-8 @ no__t-9computer @ no__t-10 @ no__t @ no__t-12 @ no__t-13groupname @ no__t-14 @ no__t-15, &gt;6 @ no__t-17computer @ no__t-18 @ no__t @ no__t-20 @ no__t-21groupname @ no__t-22 @ no__t-23、または \\4computer @ no__t-25 @ no__t-26 @ no__t-27 @ no__t-28groupname @ no__t-29 @ no__t-30
-   UNIX ユーザーの場合は、&lt;Nis ドメイン @ no__t @ no__t @ no__t @ no__t-4 の形式を使用します。 &lt;user name @ no__t-6 @ no__t @ no__t-8Nis Domain @ no__t-9、user &gt;0name @ no__t-11 @ no__t-12、または PCNFS @ no__t-13 @ no__t-14user name @ no__t-15
-   UNIX グループの場合、&lt;Nis Domain @ no__t @ no__t @ no__t @ no__t-3groupname @ no__t-4、&lt;groupname @ no__t-6 @ no__t-7 @ no__t-8Nis Domain @ no__t-9、&gt;0groupname @ no__t-11 @ no__t-12、または PCNFS @ no__t-13 @ no__t-14groupname @-15

## <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
