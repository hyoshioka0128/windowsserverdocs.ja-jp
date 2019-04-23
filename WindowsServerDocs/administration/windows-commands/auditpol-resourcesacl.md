---
title: auditpol resourceSACL
description: Windows コマンド」のトピック**uditpol resourceSACL** -グローバル リソース システム アクセス制御リスト (Sacl) を構成します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 375f37250404dd6740027cb18959697626c1ffc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837493"
---
# <a name="auditpol-resourcesacl"></a>auditpol resourceSACL



グローバル リソース システム アクセス制御リスト (Sacl) を構成します。

> [!NOTE]
> 7 および Windows Server 2008 R2、Windows にのみ適用されます。

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
|/set|新しいエントリを追加または既存のリソースのリソースの SACL エントリを更新する指定された型。|
|/remove|グローバル オブジェクト アクセスの一覧を監査内の特定のユーザーのすべてのエントリを削除します。|
|/clear|グローバル オブジェクト アクセスの一覧を監査からすべてのエントリを削除します。|
|/view|リソースの SACL のグローバル オブジェクト アクセスの監査エントリを一覧表示します。 ユーザーおよびリソースの種類は省略可能です。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="arguments"></a>引数

|引数|説明|
|--------|-----------|
|/型|オブジェクト アクセスの監査が構成されてリソースです。 サポートされている引数の値は、(ディレクトリとファイル) 用のファイルと (レジストリ キー) のキーです。</br>注:ファイルとキーの値は大文字小文字を区別します。|
|/success|成功の監査を指定します。|
|/failure|失敗の監査を指定します。|
|/user|次の形式のいずれかでは、ユーザーを指定します。</br>-DomainName\Account (DOM\Administrators) など</br>-StandaloneServer\Group アカウント (を参照してください[LookupAccountName 関数](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx))</br>-{S-1-x-x-x-x} (x はの 10 進数で表され全体の SID は、中かっこで囲む必要があります)。例: {S-1-5-21-5624481-130208933-164394174-1001}</br>    注:   SID の形式を使用する場合、このアカウントの存在を確認するチェックは行われません。|
|されます/access|2 つの形式のいずれかで指定できるアクセス許可マスクを指定します。</br>-シンプルな権限のシーケンス。</br>    -汎用アクセス権限:</br>        GA - すべてのジェネリック</br>        -GR: 汎用読み取り</br>        -GW: 汎用書き込み</br>        -GX - 汎用の実行します。</br>    ファイルのアクセス権限。</br>        -FA - ファイルのすべてのアクセス</br>        汎用 - FR - ファイルの読み取り</br>        -FW - ファイルの汎用書き込み</br>        -FX - ファイルの汎用を実行します。</br>    レジストリ キーのアクセス権限:</br>        -KA - キーのすべてのアクセス</br>        -韓国 - キーの読み取り</br>        -KW - キーの書き込み</br>        -KX - キーを実行します。</br>    例: '/アクセス: FRFW' は読み取りのイベントの監査を有効にして、書き込み操作</br>(0x1200a9) などのアクセス マスクを表す-16 進数の値</br>    これは、セキュリティ記述子定義言語 (SDDL) 標準の一部ではないリソースに固有のビット マスクを使用する場合に便利です。 省略すると、フル アクセスが使用されます。|

## <a name="remarks"></a>注釈

ResourceSACL 操作では、そのオブジェクトのセキュリティ記述子の設定で書き込みまたはフル コントロール権限が必要です。 所有することによって、resourceSACL 操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、削除操作を実行する必要はありません、追加のアクセスを許可します。

## <a name="BKMK_Examples"></a>例

成功したアクセスを監査する SACL はグローバル リソースを設定するには、レジストリ キーのユーザー回数します。
```
auditpol /resourceSACL /set /type:Key /user:MYDOMAIN\myuser /success
```
グローバル リソース汎用読み取りを実行し、ファイルまたはフォルダーの関数を記述するためのユーザーによって成功および失敗した試行を監査 SACL を設定するには。
```
auditpol /resourceSACL /set /type:File /user:MYDOMAIN\myuser /success /failure /access:FRFW
```
ファイルまたはフォルダーのすべてのグローバル リソース SACL のエントリを削除するには。
```
auditpol /resourceSACL /type:File /clear
```
ファイルまたはフォルダーから特定のユーザーのすべてのグローバル リソース SACL エントリを削除します。
```
auditpol /resourceSACL /remove /type:File /user:{S-1-5-21-56248481-1302087933-1644394174-1001}
```
グローバル オブジェクト アクセスの監査エントリをファイルまたはフォルダーの設定を一覧表示します。
```
auditpol /resourceSACL /type:File /view
```
ボックスの一覧には、グローバル オブジェクトは、ファイルまたはフォルダーに設定されている特定のユーザーの監査エントリをアクセスします。
```
auditpol /resourceSACL /type:File /view /user:MYDOMAIN\myuser
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)