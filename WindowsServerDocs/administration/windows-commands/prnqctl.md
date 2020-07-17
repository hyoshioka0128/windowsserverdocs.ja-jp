---
title: prnqctl
description: Prnqctl.vbs コマンドの参照記事。テストページを印刷し、プリンターを一時停止または再開します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 7bcc6a36fb2387a82e25afd41be2d22615565bfe
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931151"
---
# <a name="prnqctl"></a>prnqctl

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

テスト ページを印刷を一時停止や、プリンターが再開プリンター キューをクリアします。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて prnqctl.vbs ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl`。

## <a name="syntax"></a>構文

```
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <Servername>] [-p <Printername>] [-u <Username>] [-w <password>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -Z | **-P**パラメーターによって指定されたプリンターの印刷を一時停止します。 |
| -M | **-P**パラメーターによって指定されたプリンターの印刷を再開します。 |
| -E | **-P**パラメーターによって指定されたプリンターにテストページを印刷します。 |
| -X | **-P**パラメーターによって指定されたプリンターのすべての印刷ジョブをキャンセルします。 |
| -s`<Servername>` | 管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| -p`<Printername>` | 必須です。 管理するプリンターの名前を指定します。 |
| -u `<Username>` -w`<password>` | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドが機能するように、これらのアクセス許可を持つアカウントでログオンする必要があります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例、"コンピューター名")。

### <a name="examples"></a>例

Server1 コンピューターによって共有されている Laserprinter1 プリンターでテストページを印刷するには \\ 、次のように入力します。

```
cscript prnqctl -e -s Server1 -p Laserprinter1
```

ローカルコンピューター上の Laserprinter1 プリンターで印刷を一時停止するには、次のように入力します。

```
cscript prnqctl -z -p Laserprinter1
```

ローカルコンピューター上の Laserprinter1 プリンターのすべての印刷ジョブをキャンセルするには、次のように入力します。

```
cscript prnqctl -x -p Laserprinter1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
