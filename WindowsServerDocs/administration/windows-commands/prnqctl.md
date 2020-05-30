---
title: prnqctl
description: テストページを印刷するか、プリンターを一時停止または再開します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 3e18a9c0321197887b1f708854a130f41b41e7a7
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222032"
---
# <a name="prnqctl"></a>prnqctl

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

テスト ページを印刷を一時停止や、プリンターが再開プリンター キューをクリアします。

## <a name="syntax"></a>構文
```
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <ServerName>]
[-p <printerName>] [-u <UserName>] [-w <Password>]
```
### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|-Z|**-p**パラメーターを使用して指定されたプリンターの印刷を一時停止します。|
|-M|指定されているプリンタで印刷を再開、 **-p** パラメーター。|
|-E|**-p**パラメーターを使用して指定されたプリンターにテストページを印刷します。|
|-X|指定されているプリンタのすべての印刷ジョブが取り消される、 **-p** パラメーター。|
|-s\<ServerName>|管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。|
|-p\<printerName>|管理するプリンターの名前を指定します。 必須です。|
|-u \<UserName> -w\<Password>|管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>解説
- **Prnqctl.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts ディレクトリにある Visual Basic スクリプトです \\ <language> 。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prnqctl.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例:
  ```
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl
  ```
- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (たとえば、 `"computer Name"` )。

## <a name="examples"></a><a name="BKMK_examples"></a>例
\ Server1 コンピューターで共有されている Laserprinter1 プリンターでテストページを印刷するには \\ 、次のように入力します。
```
cscript Prnqctl -e -s Server1 -p Laserprinter1
```
ローカルコンピューター上の Laserprinter1 プリンターで印刷を一時停止するには、次のように入力します。
```
cscript Prnqctl -z -p Laserprinter1
```
ローカルコンピューター上の Laserprinter1 プリンターのすべての印刷ジョブをキャンセルするには、次のように入力します。
```
cscript Prnqctl -x -p Laserprinter1
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[印刷コマンドのリファレンス](print-command-reference.md)
