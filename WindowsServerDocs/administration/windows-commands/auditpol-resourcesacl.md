---
title: auditpol resourceSACL
description: リソースシステムアクセス制御リスト (Sacl) を構成する auditpol resourceSACL コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1c33a82b34c803961abff6ee5a9693990a0ca00
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923707"
---
# <a name="auditpol-resourcesacl"></a>auditpol resourceSACL

> 適用対象: Windows 7 および Windows Server 2008 R2

グローバルリソースシステムアクセス制御リスト (Sacl) を構成します。

*Resourcesacl*操作を実行するには、セキュリティ記述子でそのオブジェクトセットの**書き込み**または**フルコントロール**のアクセス許可を持っている必要があります。 **監査とセキュリティログの管理**(SeSecurityPrivilege) ユーザー権限を持っている場合は、 *resourcesacl*操作を実行することもできます。

## <a name="syntax"></a>構文

```
auditpol /resourceSACL
[/set /type:<resource> [/success] [/failure] /user:<user> [/access:<access flags>]]
[/remove /type:<resource> /user:<user> [/type:<resource>]]
[/clear [/type:<resource>]]
[/view [/user:<user>] [/type:<resource>]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /set | 指定されたリソースの種類について、リソースの SACL 内の既存のエントリを追加または更新します。 |
| /remove | グローバルオブジェクトアクセスの監査一覧で、指定されたユーザーのすべてのエントリを削除します。 |
| /clear | グローバルオブジェクトアクセスの監査リストからすべてのエントリを削除します。|
| /view | リソース SACL のグローバルオブジェクトアクセスの監査エントリを一覧表示します。 ユーザーおよびリソースの種類は省略可能です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="arguments"></a>引数

| 引数 | 説明 |
| -------- | ----------- |
| /type | オブジェクトアクセスの監査を構成する対象のリソース。 サポートされている、大文字と小文字を区別する引数の値は、*ファイル*(ディレクトリおよびファイルの場合) と*キー* (レジストリキーの場合) です。 |
| /success | 成功の監査を指定します。 |
| /failure | 失敗の監査を指定します。 |
| /user | 次のいずれかの形式のユーザーを指定します。<ul><li> DomainName\Account (Dom\ 管理者など)</li><li>スタンドアロングループアカウント (「 [LookupAccountName 関数](https://docs.microsoft.com/windows/win32/api/winbase/nf-winbase-lookupaccountnamea)」を参照)</li><li>{S-1-x-x-x}(x は10進数で表され、SID 全体は中かっこで囲む必要があります)。 例: {S-1-5-21-5624481-130208933-164394174-1001}<p>**注:** SID フォームが使用されている場合、このアカウントの存在を確認するためのチェックは行われません。</li></ul> |
| /アクセス | で指定できるアクセス許可マスクを指定します。<p>一般的なアクセス権 (以下を含む):<ul><li>GA-汎用すべて</li><li>GR-汎用読み取り</li><li>GW-汎用書き込み</li><li>GX-汎用実行</li></ul><p>ファイルのアクセス権 (次のものを含む):<ul><li>FA-すべてのファイルへのアクセス</li><li>ファイルの一般読み取り</li><li>FW-ファイルの汎用書き込み</li><li>FX-ファイルの汎用実行</li></ul><p>次のようなレジストリキーのアクセス権<ul><li>KA-キーのすべてのアクセス</li><li>韓国-キーの読み取り</li><li>KW キーの書き込み</li><li>KX キーの実行</li></ul><p>たとえば、は `/access:FRFW` 、読み取りおよび書き込み操作の監査イベントを有効にします。<p>アクセスマスクを表す16進数の値 (0x1200a9 など)<p>これは、セキュリティ記述子定義言語 (SDDL) 標準の一部ではないリソース固有のビットマスクを使用する場合に便利です。 省略した場合は、フルアクセスが使用されます。 |

## <a name="examples"></a>例

レジストリキーに対するユーザーによる成功したアクセス試行を監査するグローバルリソース SACL を設定するには、次のようにします。

```
auditpol /resourceSACL /set /type:Key /user:MYDOMAIN\myuser /success
```

グローバルリソース SACL を設定して、ユーザーがファイルまたはフォルダーに対して汎用的な読み取りおよび書き込み関数を実行するために成功および失敗した試行を監査するには、次の手順を実行します。

```
auditpol /resourceSACL /set /type:File /user:MYDOMAIN\myuser /success /failure /access:FRFW
```

ファイルまたはフォルダーのグローバルリソース SACL エントリをすべて削除するには、次のようにします。

```
auditpol /resourceSACL /type:File /clear
```

ファイルまたはフォルダーから特定のユーザーのグローバルリソースの SACL エントリをすべて削除するには、次のようにします。

```
auditpol /resourceSACL /remove /type:File /user:{S-1-5-21-56248481-1302087933-1644394174-1001}
```

ファイルまたはフォルダーに設定されたグローバルオブジェクトアクセスの監査エントリを一覧表示するには、次のようにします。

```
auditpol /resourceSACL /type:File /view
```

ファイルまたはフォルダーに設定されている特定のユーザーのグローバルオブジェクトアクセスの監査エントリを一覧表示するには、次のようにします。

```
auditpol /resourceSACL /type:File /view /user:MYDOMAIN\myuser
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [auditpol コマンド](auditpol.md)
