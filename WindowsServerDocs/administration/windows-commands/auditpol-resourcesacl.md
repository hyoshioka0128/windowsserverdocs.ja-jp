---
title: auditpol resourceSACL
description: リソースシステムアクセス制御リスト (Sacl) を構成する**Auditpol resourceSACL**の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b004be6f21cd076fe20e73c45268731c35d654e5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851155"
---
# <a name="auditpol-resourcesacl"></a>auditpol resourceSACL

グローバルリソースシステムアクセス制御リスト (Sacl) を構成します。

> [!NOTE]
> Windows 7 および Windows Server 2008 R2 にのみ適用されます。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

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
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="arguments"></a>引数

| 引数 | 説明 |
| -------- | ----------- | 
| /type | オブジェクトアクセスの監査を構成する対象のリソース。 サポートされている、大文字と小文字を区別する引数の値は、ファイル (ディレクトリおよびファイルの場合) とキー (レジストリキーの場合) です。 |
| /success | 成功の監査を指定します。 |
| /failure | 失敗の監査を指定します。 |
| /user | 次のいずれかの形式のユーザーを指定します。<ul><li> DomainName\Account (Dom\ 管理者など)</li><li>スタンドアロングループアカウント (「 [LookupAccountName 関数](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx)」を参照)</li><li>{S-1-x-x-x}(x は10進数で表され、SID 全体は中かっこで囲む必要があります)。 例: {S-1-5-21-5624481-130208933-164394174-1001}<p>**注:** SID フォームが使用されている場合、このアカウントの存在を確認するためのチェックは行われません。</li></ul> |
| /アクセス | で指定できるアクセス許可マスクを指定します。<p>一般的なアクセス権 (以下を含む):<ul><li>GA-汎用すべて</li><li>GR-汎用読み取り</li><li>GW-汎用書き込み</li><li>GX-汎用実行</li></ul><p>ファイルのアクセス権 (次のものを含む):<ul><li>FA-すべてのファイルへのアクセス</li><li>ファイルの一般読み取り</li><li>FW-ファイルの汎用書き込み</li><li>FX-ファイルの汎用実行</li></ul><p>次のようなレジストリキーのアクセス権<ul><li>KA-キーのすべてのアクセス</li><li>韓国-キーの読み取り</li><li>KW キーの書き込み</li><li>KX キーの実行</li></ul><p>たとえば、`/access:FRFW` は、読み取りおよび書き込み操作の監査イベントを有効にします。<p>アクセスマスクを表す16進数の値 (0x1200a9 など)<p>    これは、セキュリティ記述子定義言語 (SDDL) 標準の一部ではないリソース固有のビットマスクを使用する場合に便利です。 省略した場合は、フルアクセスが使用されます。 |

## <a name="remarks"></a>コメント

ResourceSACL 操作の場合は、セキュリティ記述子で設定されたそのオブジェクトに対する書き込みまたはフルコントロールのアクセス許可が必要です。 また、**監査とセキュリティログの管理**(SeSecurityPrivilege) ユーザー権利を所有することによって、resourcesacl 操作を実行することもできます。 ただし、この権限により、削除操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="examples"></a><a name=BKMK_Examples></a>例

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