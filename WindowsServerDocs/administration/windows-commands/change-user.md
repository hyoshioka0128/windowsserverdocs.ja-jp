---
title: change user
description: '[ユーザーの変更] コマンドのリファレンストピックでは、リモートデスクトップセッションホストサーバーのインストールモードを変更します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6202f024-8cf5-411e-89b1-ee37ff46499d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ae082ebd2b5cf98be891d8f557f9e42d7724d22
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716093"
---
# <a name="change-user"></a>change user

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホストサーバーのインストールモードを変更します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、「 [Windows Server でのリモートデスクトップサービスの新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))機能」を参照してください。

## <a name="syntax"></a>構文

```
change user {/execute | /install | /query}
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| /execute | .Ini ファイルをホームディレクトリにマッピングできるようにします。 これが既定の設定です。 |
| /install | .Ini ファイルのホームディレクトリへのマッピングを無効にします。 すべての .ini ファイルが読み取られ、システムディレクトリに書き込まれます。 リモートデスクトップセッションホストサーバーにアプリケーションをインストールする場合は、.ini ファイルマッピングを無効にする必要があります。 |
| /query | .Ini ファイルマッピングの現在の設定を表示します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- アプリケーションをインストールする前に、 **change user/install**を使用して、アプリケーションの .ini ファイルをシステムディレクトリに作成します。 これらのファイルは、ユーザー固有の .ini ファイルが作成されるときにソースとして使用されます。 アプリケーションをインストールしたら、 **change user/execute**を使用して、標準 .ini ファイルマッピングに戻します。

- アプリを初めて実行するときに、ホームディレクトリで .ini ファイルが検索されます。 .Ini ファイルがホームディレクトリに見つからず、system ディレクトリにある場合は、リモートデスクトップサービスによって、.ini ファイルがホームディレクトリにコピーされ、各ユーザーがアプリケーションの .ini ファイルのコピーを一意に持つことができます。 新しい .ini ファイルがホームディレクトリに作成されます。

- 各ユーザーは、アプリケーションの .ini ファイルの一意のコピーを持っている必要があります。 これにより、異なるユーザーがアプリケーション構成に互換性のないインスタンスを持つ可能性があります (たとえば、既定のディレクトリや画面の解像度が異なる)。

- システムで**change user/install**が実行されている場合、いくつかの処理が行われます。 作成されたすべてのレジストリエントリは、 **\Software\microsoft\windows NT\Currentversion\Terminal のインストール**で、 **\ software**サブキーまたは**\ MACHINE**サブキーの HKEY_LOCAL_MACHINE 下にシャドウされます。 **HKEY_CURRENT_USER**に追加されたサブキーは、 **\ software**サブキーの下にコピーされ、 **HKEY_LOCAL_MACHINE**に追加されたサブキーは**\ マシン**サブキーの下にコピーされます。 アプリケーションが GetWindowsdirectory などのシステムコールを使用して Windows ディレクトリに対してクエリを行う場合、rd セッションホストサーバーは systemroot ディレクトリを返します。 WritePrivateProfileString などのシステムコールを使用して .ini ファイルのエントリが追加された場合、そのエントリは、systemroot ディレクトリの .ini ファイルに追加されます。

- システムがを返して**ユーザー/execute を変更**しようとしたときに、アプリケーションが存在しない**HKEY_CURRENT_USER**の下にあるレジストリエントリを読み取ろうとすると、リモートデスクトップサービスによって、 **\ Terminal \ インストール**サブキーの下にキーのコピーが存在するかどうかが確認されます。 その場合、サブキーは**HKEY_CURRRENT_USER**の下の適切な場所にコピーされます。 アプリケーションが存在しない .ini ファイルから読み取ろうとした場合は、リモートデスクトップサービスシステムルートの下でその .ini ファイルを検索します。 .Ini ファイルがシステムルート内にある場合は、ユーザーのホームディレクトリの \Windows サブディレクトリにコピーされます。 アプリケーションが Windows ディレクトリに対してクエリを行う場合、rd セッションホストサーバーは、ユーザーのホームディレクトリの \Windows サブディレクトリを返します。

- ログオンすると、リモートデスクトップサービスによって、コンピューター上の .ini ファイルよりもシステムの .ini ファイルが新しいかどうかがチェックされます。 システムのバージョンが新しい場合は、.ini ファイルが置き換えられるか、新しいバージョンにマージされます。 これは、この .ini ファイルに INISYNC ビット0x40 が設定されているかどうかによって異なります。 以前のバージョンの .ini ファイルは、Inifile という名前に変更されています。 **\ Terminal \ インストール**サブキーの下にあるシステムレジストリ値が**HKEY_CURRENT_USER**の下のバージョンより新しい場合は、サブキーのバージョンが削除され、 **\ terminal \ インストール**の新しいサブキーに置き換えられます。

## <a name="examples"></a>例

- .Ini ファイルマッピングをホームディレクトリで無効にするには、次のように入力します。

  ```
  change user /install
  ```

- ホームディレクトリで .ini ファイルマッピングを有効にするには、次のように入力します。

  ```
  change user /execute
  ```

- .Ini ファイルマッピングの現在の設定を表示するには、次のように入力します。

  ```
  change user /query
  ```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コマンドの変更](change.md)

- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
