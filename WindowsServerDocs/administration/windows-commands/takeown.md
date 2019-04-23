---
title: takeown
description: ファイルの所有者になるファイルへのアクセスを取得する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b5a4874edf9fa4406d4643e686fed2b725699dd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854363"
---
# <a name="takeown"></a>takeown

管理者をファイルの所有者にすることによって、拒否されていたファイルへの管理者のアクセスを回復できます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
takeown [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <File name> [/a] [/r [/d {Y|N}]]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<コンピューター >|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定値はローカル コンピューターです。 このパラメーターは、すべてのファイルと、コマンドで指定されたフォルダーに適用されます。|
|/u [\<ドメイン >\]<User name>|指定したユーザー アカウントのアクセス許可を持つ、スクリプトを実行します。 既定値は、システムのアクセス許可です。|
|/p [\<パスワード >]|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/f\<ファイル名 >|ファイル名またはディレクトリの名前を指定のパターン。 ワイルドカード文字を使用することができます * のパターンを指定する場合。 構文を使用することもできます。 *ShareName*\*FileName *。|
|/a|現在のユーザーの代わりに、Administrators グループに所有権を示します。|
|/r|指定したディレクトリとサブディレクトリ内のすべてのファイルに対して再帰的な操作を実行します。|
|/d {Y \| N}|現在のユーザーが指定したディレクトリに対するフォルダー一覧表示"アクセス許可がないし、指定された既定値を代わりに使用するときに表示される確認のプロンプトを表示しません。 有効な値、 **/d** オプションは次のようにします。</br>「Y」ディレクトリの所有権を取得します。</br>-N:ディレクトリをスキップします。</br>と共にこのオプションを使用する必要がありますに注意してください、 **/r** オプション。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   このコマンドは通常、バッチ ファイルで使用されます。
-   場合、 **/a** パラメーターが指定されていない、現在コンピューターにログオンしているユーザーにファイルの所有権が与えられます。
-   使用した混合のパターン (**でしょうか。** **&#42;**) でサポートされていない**takeown**コマンド。
-   ロックを削除した後は **takeown**, 、Windows エクスプ ローラーを使用する必要がありますまたは **cacls** されるように完全なアクセス許可、ファイルとディレクトリを削除するにはコマンドです。 詳細については **cacls**, 、このトピックの最後に「その他の参照」を参照してください。

## <a name="BKMK_examples"></a>例

Lostfile という名前のファイルの所有権を取得するには、次のように入力します。
```
takeown /f lostfile
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)