---
title: auditpol resourceSACL
description: '**Uditpol resourceSACL**の Windows コマンドトピック-グローバルリソースシステムアクセス制御リスト (sacl) を構成します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2acffd75298f0f36a9c15e0622816feaae57cb64
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382429"
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

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/set|指定されたリソースの種類について、リソースの SACL 内の既存のエントリを追加または更新します。|
|/remove|グローバルオブジェクトアクセスの監査一覧で、指定されたユーザーのすべてのエントリを削除します。|
|/clear|グローバルオブジェクトアクセスの監査リストからすべてのエントリを削除します。|
|/view|リソース SACL のグローバルオブジェクトアクセスの監査エントリを一覧表示します。 ユーザーおよびリソースの種類は省略可能です。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="arguments"></a>引数

|引数|説明|
|--------|-----------|
|/type|オブジェクトアクセスの監査を構成する対象のリソース。 サポートされている引数の値は、ファイル (ディレクトリおよびファイルの場合) とキー (レジストリキーの場合) です。</br>メモ:ファイルとキーの値では大文字と小文字が区別されます。|
|/success|成功の監査を指定します。|
|/failure|失敗の監査を指定します。|
|/user|次のいずれかの形式のユーザーを指定します。</br>-DomainName\Account (Dom\ 管理者など)</br>-スタンドアロンアカウント (「 [LookupAccountName 関数](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx)」を参照)</br>-{S-1-x-x-x} (x は10進数で表され、SID 全体は中かっこで囲む必要があります)。例: {S-1-5-21-5624481-130208933-164394174-1001}</br>    メモ:   SID フォームが使用されている場合、このアカウントの存在を確認するためのチェックは行われません。|
|/アクセス|次の2つの形式のいずれかで指定できるアクセス許可マスクを指定します。</br>-単純な権限のシーケンス。</br>    -汎用アクセス権:</br>        -GA-汎用すべて</br>        -GR-汎用読み取り</br>        -GW-汎用書き込み</br>        -GX-汎用実行</br>    -ファイルのアクセス権:</br>        -FA-すべてのファイルへのアクセス</br>        -FR-ファイルの一般読み取り</br>        -FW-FILE 汎用書き込み</br>        -FX-ファイル汎用実行</br>    -レジストリキーのアクセス権:</br>        -KA-キーのすべてのアクセス</br>        -韓国-キーの読み取り</br>        -KW キーの書き込み</br>        -KX キーの実行</br>    たとえば、"/access: FRFW" は、読み取りおよび書き込み操作の監査イベントを有効にします。</br>-アクセスマスクを表す16進数の値 (0x1200a9 など)</br>    これは、セキュリティ記述子定義言語 (SDDL) 標準の一部ではないリソース固有のビットマスクを使用する場合に便利です。 省略した場合は、フルアクセスが使用されます。|

## <a name="remarks"></a>コメント

ResourceSACL 操作の場合は、セキュリティ記述子で設定されたそのオブジェクトに対する書き込みまたはフルコントロールのアクセス許可が必要です。 また、**監査とセキュリティログの管理**(SeSecurityPrivilege) ユーザー権利を所有することによって、resourcesacl 操作を実行することもできます。 ただし、この権限により、削除操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="BKMK_Examples"></a>例

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

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)