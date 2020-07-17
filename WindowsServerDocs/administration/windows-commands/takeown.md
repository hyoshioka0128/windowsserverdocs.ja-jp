---
title: takeown
description: ファイルの所有者になることによってファイルにアクセスする方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da43b13f0333f3a12a8763db4cad31e12283bb8b
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436197"
---
# <a name="takeown"></a>takeown

管理者をファイルの所有者にすることによって、拒否されていたファイルへの管理者のアクセスを回復できます。



## <a name="syntax"></a>構文

```
takeown [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <File name> [/a] [/r [/d {Y|N}]]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s \< コンピューター>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定値はローカル コンピューターです。 このパラメーターは、すべてのファイルと、コマンドで指定されたフォルダーに適用されます。|
|/u [ \< ドメイン>\]<User name>|指定したユーザー アカウントのアクセス許可を持つ、スクリプトを実行します。 既定値は、システムのアクセス許可です。|
|/p [ \< パスワード>]|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|/f \< ファイル名>|ファイル名またはディレクトリの名前を指定のパターン。 パターンを指定するときは、ワイルドカード文字 * を使用できます。 また、構文*ShareName*FileName * を使用することもでき \* ます。|
|/a|現在のユーザーの代わりに、Administrators グループに所有権を示します。|
|/r|指定したディレクトリとサブディレクトリ内のすべてのファイルに対して再帰的な操作を実行します。|
|/d {Y \| N}|現在のユーザーが指定したディレクトリに対するフォルダー一覧表示"アクセス許可がないし、指定された既定値を代わりに使用するときに表示される確認のプロンプトを表示しません。 有効な値、 **/d** オプションは次のようにします。</br>に「y」は、ディレクトリ所有権を取得します。</br>ディレクトリをスキップします。</br>と共にこのオプションを使用する必要がありますに注意してください、 **/r** オプション。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>解説

-   このコマンドは通常、バッチ ファイルで使用されます。
-   場合、 **/a** パラメーターが指定されていない、現在コンピューターにログオンしているユーザーにファイルの所有権が与えられます。
-   使用した混合のパターン (**でしょうか。** および **&#42;**) は、 **takeown**コマンドではサポートされていません。
-   ロックを削除した後は **takeown**, 、Windows エクスプ ローラーを使用する必要がありますまたは **cacls** されるように完全なアクセス許可、ファイルとディレクトリを削除するにはコマンドです。 **Cacls**の詳細については、このトピックの最後にある「その他の参照情報」を参照してください。

## <a name="examples"></a><a name="BKMK_examples"></a>例

Lostfile という名前のファイルの所有権を取得するには、次のように入力します。
```
takeown /f lostfile
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)