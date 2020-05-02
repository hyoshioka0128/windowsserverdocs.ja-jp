---
title: mapadmin
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19975f6f4e0e49cf55e4e80f6566f8596d6d33d8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724024"
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

&lt;コンピューター&gt;管理するユーザー名マッピングサービスを実行しているリモートコンピューターを指定します。 Windows インターネットネームサービス (WINS) 名またはドメインネームシステム (DNS) 名またはインターネットプロトコル (IP) アドレスを使用して、コンピューターを指定できます。

-u &lt;ユーザー&gt;資格情報を使用するユーザーのユーザー名を指定します。 ドメイン**\\**<em>ユーザー名</em>と<em>いう形式の</em>ユーザー名にドメイン名を追加する必要がある場合があります。

-p &lt;password&gt;ユーザーのパスワードを指定します。 - **U**オプションを指定しても **-p**オプションを省略した場合、ユーザーのパスワードの入力を求められます。
**Mapadmin**が実行する特定のアクションは、指定するコマンド引数によって異なります。

### <a name="parameters"></a>パラメーター
### <a name="start"></a>start
ユーザー名マッピングサービスを開始します。

### <a name="stop"></a>stop
ユーザー名マッピングサービスを停止します。

### <a name="config"></a>config
ユーザー名マッピングの全般設定を指定します。 このコマンド引数では、次のオプションを使用できます。 **- &lt;r&lt;dddd&gt; &gt;:&lt;&gt;hh: mm** -Windows および NIS データベースから更新する更新間隔を日、時間、分単位で指定します。 最小間隔は5分です。
**-i {yes | no}** -単純なマッピングをオン (**はい**) またはオフ (**いいえ**) にします。 既定では、単純なマッピングはオンになっています。
[**追加**]: ユーザーまたはグループの新しいマッピングを作成します。 このコマンド引数では、次のオプションを使用できます。

|オプション|定義|
|-----|-------|
|-wu &lt;名&gt;|新しいマッピングを作成する Windows ユーザーの名前を指定します。|
|-uu &lt;名&gt;|新しいマッピングを作成する UNIX ユーザーの名前を指定します。|
|-wg &lt;グループ&gt;|新しいマッピングを作成する Windows グループの名前を指定します。|
|-ug &lt;グループ&gt;|新しいマッピングを作成する UNIX グループの名前を指定します。|
|-setprimary|新しいマッピングがプライマリマッピングであることを指定します。|

**setprimary** -複数のマッピングを持つ UNIX ユーザーまたはグループのプライマリマッピングであるマッピングを指定します。 このコマンド引数では、次のオプションを使用できます。

|オプション|定義|
|-----|-------|
|-wu &lt;名&gt;|プライマリマッピングの Windows ユーザーを指定します。 ユーザーに対して複数のマッピングが存在する場合は、 **-uu**オプションを使用してプライマリマッピングを指定します。|
|-uu &lt;名&gt;|プライマリマッピングの UNIX ユーザーを指定します。|
|-wg &lt;グループ&gt;|プライマリマッピングの Windows グループを指定します。 グループに対して複数のマッピングが存在する場合は、 **-ug**オプションを使用してプライマリマッピングを指定します。|
|-ug &lt;グループ&gt;|プライマリマッピングの UNIX グループを指定します。|

**削除**-ユーザーまたはグループのマッピングを削除します。 このコマンド引数には、次のオプションを使用できます。

|オプション|定義|
|-----|-------|
|-wu &lt;ユーザー&gt;|Windows &lt; *&gt;ドメイン\\ユーザー名&gt;として指定された、マッピングを削除する対象の Windows&lt;* ユーザー。 **-Wu**または **-uu**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Wu**オプションのみを指定すると、指定したユーザーのすべてのマッピングが削除されます。|
|-wg &lt;グループ&gt;|マッピングが削除される Windows グループ。 windowsdomain &lt;&gt;\\&lt;groupname&gt;として指定されます。 **-Wg**または **-ug**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Wg**オプションのみを指定すると、指定したグループのすべてのマッピングが削除されます。|
|-uu &lt;user&gt;|マッピングが削除される UNIX ユーザー。ユーザー名&lt;&gt;として指定されます。 **-Wu**または **-uu**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Uu**オプションのみを指定すると、指定したユーザーのすべてのマッピングが削除されます。|
|-ug &lt;グループ&gt;|マッピングが削除される UNIX グループ。 groupname &lt;&gt;として指定されます。 **-Wg**または **-ug**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Ug**オプションのみを指定すると、指定したグループのすべてのマッピングが削除されます。|

**リスト**-ユーザーとグループのマッピングに関する情報を表示します。 このコマンド引数では、次のオプションを使用できます。

|オプション|定義|
|-----|-------|
|-すべて|ユーザーとグループの単純なマッピングと高度なマッピングの両方を一覧表示します。|
|-シンプル|すべての単純なマップされたユーザーとグループを一覧表示します。|
|-詳細設定|すべての高度なマップされたユーザーとグループを一覧表示します。 マップは、評価される順序で一覧表示されます。 アスタリスク (*) が付いたプライマリマップが最初に一覧表示され、次にセカンダリマップがカラット (^) でマークされます。|
|-wu &lt;名&gt;|指定された Windows ユーザーのマッピングを一覧表示します。|
|-wg &lt;グループ&gt;|Windows グループのマッピングを一覧表示します。|
|-uu &lt;名&gt;|UNIX ユーザーのマッピングを一覧表示します。|
|-ug &lt;グループ&gt;|UNIX グループのマッピングを一覧表示します。|

**バックアップ**-ユーザー名マッピングの構成とマッピングデータを filename &lt;&gt;で指定されたファイルに保存します。
**復元**-構成およびマッピングデータを、 **backup** command 引数を使用して&lt;作成&gt;されたファイル (filename で指定) のデータに置き換えます。
**adddomainmap** -Windows ドメインと NIS ドメイン、またはパスワードとグループファイルの間に単純なマップを追加します。 このコマンド引数には、次のオプションを使用できます。

|オプション|定義|
|-----|-------|
|-d &lt;windowsdomain&gt;|マップする Windows ドメインを指定します。|
|-y &lt;nis ドメイン&gt;|マップする NIS ドメインを指定します。&lt;br/&gt;&lt;br/&gt;**-n** &lt;nis サーバー&gt; **-y**オプションで指定された nis ドメインの nis サーバーを指定します。|
|-f &lt;パス&gt;|マップするパスワードおよびグループファイルを含むディレクトリの完全修飾パスを指定します。 ファイルは、管理されているコンピューターに配置する必要があります。 **mapadmin**を使用してリモートコンピューターを管理し、パスワードおよびグループファイルに基づいてマップを設定することはできません。|

**removedomainmap** -Windows ドメインと NIS ドメインとの間の単純なマップを削除します。 このコマンド引数には、次のオプションと引数を使用できます。

|オプション|定義|
|-----|-------|
|-d &lt;windowsdomain&gt;|削除するマップの Windows ドメインを指定します。|
|-y &lt;nis ドメイン&gt;|削除するマップの NIS ドメインを指定します。|
|-すべて|Windows および NIS ドメイン間のすべての単純なマップを削除することを指定します。 これにより、Windows ドメインとパスワードおよびグループファイル間の単純なマップも削除されます。|

**listdomainmaps** -NIS ドメイン、パスワード、およびグループファイルにマップされている Windows ドメインを一覧表示します。

## <a name="notes"></a>メモ
-   コマンド引数を指定しない場合、 **mapadmin**では、ユーザー名マッピングの現在の設定が表示されます。
-   ユーザー名またはグループ名を指定するすべてのオプションについて、次の形式を使用できます。
-   Windows ユーザーの場合は、[ &lt;ドメイン&gt;\\&lt;ユーザー名&gt;] \\ \\ &lt;、&gt;\\&lt;[コンピューター&gt;ユーザー \\ &lt;名&gt;\\&lt;]、&gt;[コンピューター &lt;ユーザー&gt;\\&lt;名]、または [コンピューターユーザー名] の形式を使用します。&gt;
-   Windows グループの場合は、domain &lt;&gt;\\&lt;&lt;&gt;&gt; \\ \\ &lt;groupname&gt;、computer\\&lt;groupname、computer&lt;groupname、computer\\groupname の形式を使用します。&lt;&gt;&gt;&gt;\\&gt; \\ &lt;&gt;&gt;&lt;&lt; &lt;&lt;&gt;&gt;
-   UNIX ユーザーの場合は、nis &lt;ドメイン&gt;\\&lt;&gt;ユーザー名&lt;、ユーザー名&gt;@&lt;、nis ドメイン&gt;、ユーザー &lt;名&gt;@PCNFS、または\\&lt;PCNFS ユーザー名の形式を使用します。&gt;
-   UNIX グループの場合は、nis &lt;ドメイン&gt;\\&lt;groupname&gt;、 &lt;groupname&gt;@&lt;nis domain&gt;、 &lt;groupname&gt;@PCNFS、または PCNFS\\&lt;groupname の形式を使用します。&gt;

## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)
