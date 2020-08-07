---
title: mapadmin
description: Mapadmin コマンドの参照記事。ネットワークファイルシステム用の Microsoft サービスのユーザー名マッピングを管理します。
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3334ae31b3abb85dcc3df046d8199c9b72ea3944
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886578"
---
# <a name="mapadmin"></a>mapadmin

**Mapadmin**コマンドラインユーティリティは、ネットワークファイルシステム用に Microsoft サービスを実行しているローカルコンピューターまたはリモートコンピューター上でユーザー名マッピングを管理します。 管理者の資格情報がないアカウントでログオンしている場合は、を実行するアカウントのユーザー名とパスワードを指定できます。

## <a name="syntax"></a>構文

```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <windowsuser> -uu <UNIXuser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <windowsgroup> -ug <UNIXgroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <Windowsuser> [-uu <UNIXuser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <Windowsgroup> [-ug <UNIXgroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <Windowsdomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <Windowsdomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<computer>` | 管理するユーザー名マッピングサービスを実行しているリモートコンピューターを指定します。 Windows インターネットネームサービス (WINS) 名またはドメインネームシステム (DNS) 名またはインターネットプロトコル (IP) アドレスを使用して、コンピューターを指定できます。 |
| -u`<user>` | 使用する資格情報を持つユーザーのユーザー名を指定します。 *Domain\username*という形式のユーザー名にドメイン名を追加する必要がある場合があります。 |
| -p`<password>` | ユーザーのパスワードを指定します。 - **U**オプションを指定しても **-p**オプションを省略した場合、ユーザーのパスワードの入力を求められます。 |
| `start | stop` | ユーザー名マッピングサービスを開始または停止します。 |
| config | ユーザー名マッピングの全般設定を指定します。 このパラメーターでは、次のオプションを使用できます。<ul><li>**-r `<dddd>:<hh>:<mm>` :** Windows および NIS データベースから更新する更新間隔を日、時間、分単位で指定します。 最小間隔は5分です。</li><li>**-i `{yes | no}` :** 単純なマッピングをオン (**yes**) またはオフ (**no**) にします。 既定では、マッピングが有効になっています。</li></ul> |
| add | ユーザーまたはグループの新しいマッピングを作成します。 このパラメーターでは、次のオプションを使用できます。<ul><li>**-wu `<name>` :** 新しいマッピングを作成する Windows ユーザーの名前を指定します。</li><li>**-uu `<name>` :** 新しいマッピングを作成する UNIX ユーザーの名前を指定します。</li><li>**-wg `<group>` :** 新しいマッピングを作成する Windows グループの名前を指定します。</li><li>**-ug `<group>` :** 新しいマッピングを作成する UNIX グループの名前を指定します。</li><li>**-setprimary:** 新しいマッピングがプライマリマッピングであることを指定します。</li></ul> |
| setprimary | 複数のマッピングを持つ UNIX ユーザーまたはグループのプライマリマッピングであるマッピングを指定します。 このパラメーターでは、次のオプションを使用できます。<ul><li>**-wu `<name>` :** プライマリマッピングの Windows ユーザーを指定します。 ユーザーに対して複数のマッピングが存在する場合は、 **-uu**オプションを使用してプライマリマッピングを指定します。</li><li>**-uu `<name>` :** プライマリマッピングの UNIX ユーザーを指定します。</li><li>**-wg `<group>` :** プライマリマッピングの Windows グループを指定します。 グループに対して複数のマッピングが存在する場合は、 **-ug**オプションを使用してプライマリマッピングを指定します。</li><li>**-ug `<group>` :** プライマリマッピングの UNIX グループを指定します。</li></ul> |
| delete | ユーザーまたはグループのマッピングを削除します。 このパラメーターでは、次のオプションを使用できます。<ul><li>**-wu `<user>` :** マッピングを削除する Windows ユーザーを指定します。これはとして指定し `<windowsdomain>\<username>` ます。<p>**-Wu**または **-uu**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Wu**オプションのみを指定すると、指定したユーザーのすべてのマッピングが削除されます。</li><li>**-uu `<user>` :** マッピングを削除する UNIX ユーザーを指定します。これはとして指定し `<username>` ます。<p>**-Wu**または **-uu**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Uu**オプションのみを指定すると、指定したユーザーのすべてのマッピングが削除されます。</li><li>**-wg `<group>` :** マッピングが削除される Windows グループを指定し `<windowsdomain>\<username>` ます。<p>**-Wg**または **-ug**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Wg**オプションのみを指定すると、指定したグループのすべてのマッピングが削除されます。</li><li>**-ug `<group>` :** マッピングが削除される UNIX グループを指定し `<groupname>` ます。<p>**-Wg**または **-ug**オプションのいずれかまたは両方を指定する必要があります。 両方のオプションを指定すると、2つのオプションによって識別される特定のマッピングが削除されます。 **-Ug**オプションのみを指定すると、指定したグループのすべてのマッピングが削除されます。</li></ul> |
| list | ユーザーとグループのマッピングに関する情報を表示します。 このパラメーターでは、次のオプションを使用できます。<ul><li>**-すべて:** ユーザーとグループの単純なマッピングと高度なマッピングの両方を一覧表示します。</li><li>**-単純:** すべての単純なマップされたユーザーとグループを一覧表示します。</li><li>**-詳細設定:** すべての高度なマップされたユーザーとグループを一覧表示します。 マップは、評価される順序で一覧表示されます。 アスタリスク () でマークされたプライマリマップ*が最初に表示され、次にセカンダリマップがカラットでマークされ `(^)` ます。 </li> <li>* *-wu `<name>` :** 指定された Windows ユーザーのマッピングを一覧表示します。</li><li>**-wg `<group>` :** Windows グループのマッピングを一覧表示します。</li><li>**-uu `<name>` :** UNIX ユーザーのマッピングを一覧表示します。</li><li>**-ug `<group>` :** UNIX グループのマッピングを一覧表示します。</li></ul> |
| バックアップ (backup) | によって指定されたファイルにユーザー名マッピングの構成とマッピングデータを保存し `<filename>` ます。 |
| 復元 | では `<filename>` 、**バックアップ**パラメーターを使用して作成されたファイル (で指定) のデータに構成データとマッピングデータが置き換えられます。 |
| adddomainmap | Windows ドメインと NIS ドメイン、またはパスワードとグループファイルの間に単純なマップを追加します。 このパラメーターでは、次のオプションを使用できます。<ul><li>**-d `<windowsdomain>` :** マップする Windows ドメインを指定します。</li><li>**-y `<NISdomain>` :** マップする NIS ドメインを指定します。 - **Y**オプションで指定された nis ドメインの nis サーバーを指定するには、 **-n `<NISserver>` **パラメーターを使用する必要があります。</li><li>**-f `<path>` :** マップするパスワードおよびグループファイルを含むディレクトリの完全修飾パスを指定します。 ファイルは、管理されているコンピューターに配置されている必要があります。 **mapadmin**を使用してリモートコンピューターを管理し、パスワードおよびグループファイルに基づいてマップを設定することはできません。</li></ul> |
| removedomainmap | Windows ドメインと NIS ドメインとの間の単純なマップを削除します。 このパラメーターでは、次のオプションと引数を使用できます。<ul><li>**-d `<windowsdomain>` :** 削除するマップの Windows ドメインを指定します。</li><li>**-y `<NISdomain>` :** 削除するマップの NIS ドメインを指定します。</li><li>**-すべて:** Windows および NIS ドメイン間のすべての単純なマップを削除することを指定します。 これにより、Windows ドメインとパスワードおよびグループファイル間の単純なマップも削除されます。</li></ul> |
| listdomainmaps | NIS ドメイン、パスワード、およびグループファイルにマップされている Windows ドメインを一覧表示します。 |

#### <a name="remarks"></a>Remarks

- パラメーターを指定しない場合、 **mapadmin**コマンドはユーザー名マッピングの現在の設定を表示します。

- ユーザー名またはグループ名を指定するすべてのオプションについて、次の形式を使用できます。

    - Windows ユーザーの場合は、、、 `<domain>\<username>` `\\<computer>\<username>` `\<computer>\<username>` 、またはの形式を使用します。`<computer>\<username>`

    - Windows グループの場合は、、、 `<domain>\<groupname>` `\\<computer>\<groupname>` `\<computer>\<groupname>` 、またはの形式を使用します。`<computer>\<groupname>`

    - UNIX ユーザーの場合は、、、 `<NISdomain>\<username>` `<username>@<NISdomain>` `<username>@PCNFS` 、またはの形式を使用します。`PCNFS\<username>`

    - UNIX グループの場合は、、、 `<NISdomain>\<groupname>` `<groupname>@<NISdomain>` `<groupname>@PCNFS` 、またはの形式を使用します。`PCNFS\<groupname>`

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
