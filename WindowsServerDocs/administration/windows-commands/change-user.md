---
title: change user
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6202f024-8cf5-411e-89b1-ee37ff46499d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 771e39182c17b9a6710e49eff2f5302e539bdbb5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379573"
---
# <a name="change-user"></a>change user

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバーのインストールモードを変更します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。
> ## <a name="syntax"></a>構文
> ```
> change user {/execute | /install | /query}
> ```
> ## <a name="parameters"></a>パラメーター
> 
> | パラメーター |                                                                                                 説明                                                                                                  |
> |-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | /execute  |                                                                .Ini ファイルをホームディレクトリにマッピングできるようにします。 これが既定の設定です。                                                                 |
> | /install  | .Ini ファイルのホームディレクトリへのマッピングを無効にします。 すべての .ini ファイルが読み取られ、システムディレクトリに書き込まれます。 Rd セッションホストサーバーにアプリケーションをインストールする場合は、.ini ファイルマッピングを無効にする必要があります。 |
> |  /query   |                                                                             .Ini ファイルマッピングの現在の設定を表示します。                                                                              |
> |    /?     |                                                                                     コマンド プロンプトにヘルプを表示します。                                                                                     |
> 
> ## <a name="remarks"></a>コメント
> - アプリケーションをインストールする前に、 **change user/install**を使用して、アプリケーションの .ini ファイルをシステムディレクトリに作成します。 これらのファイルは、ユーザー固有の .ini ファイルが作成されるときにソースとして使用されます。 アプリケーションをインストールしたら、 **change user/execute**を使用して、標準 .ini ファイルマッピングに戻します。
> - アプリケーションを初めて実行するときに、ホームディレクトリで .ini ファイルが検索されます。 .Ini ファイルがホームディレクトリに見つからず、system ディレクトリにある場合は、リモートデスクトップサービスによって、.ini ファイルがホームディレクトリにコピーされ、各ユーザーがアプリケーションの .ini ファイルのコピーを一意に持つことができます。 新しい .ini ファイルがホームディレクトリに作成されます。
> - 各ユーザーは、アプリケーションの .ini ファイルの一意のコピーを持っている必要があります。 これにより、異なるユーザーがアプリケーション構成に互換性のないインスタンスを持つ可能性があります (たとえば、既定のディレクトリや画面の解像度が異なる)。
> - システムがインストールモードの場合 (つまり、**ユーザー/install が変更**された場合)、いくつかの処理が行われます。 作成されたすべてのレジストリエントリは、 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentversion\Terminal のインストール**で、 **\ software**サブキーまたは **\ MACHINE**サブキーの下にシャドウされます。 **HKEY_CURrenT_USER**に追加されたサブキーは、 **\ software**サブキーの下にコピーされ、 **HKEY_LOCAL_MACHINE**に追加されたサブキーは **\ MACHINE**サブキーの下にコピーされます。 アプリケーションが GetWindowsdirectory などのシステムコールを使用して Windows ディレクトリに対してクエリを行う場合、rd セッションホストサーバーは systemroot ディレクトリを返します。 WritePrivateProfileString などのシステムコールを使用して .ini ファイルのエントリが追加された場合、そのエントリは、systemroot ディレクトリの .ini ファイルに追加されます。
> - システムが実行モードに戻ったとき (つまり、**ユーザー/execute が変更**された場合)、アプリケーションは、存在しない**HKEY_CURrenT_USER**の下にあるレジストリエントリを読み取ろうとすると、キーのコピーが存在するかどうかを確認リモートデスクトップサービスます。 **\ Terminal のインストール**サブキー。 その場合、サブキーが**HKEY_CURrenT_USER**の下の適切な場所にコピーされます。 アプリケーションが存在しない .ini ファイルから読み取ろうとした場合は、リモートデスクトップサービスシステムルートの下でその .ini ファイルを検索します。 .Ini ファイルがシステムルート内にある場合は、ユーザーのホームディレクトリの \Windows サブディレクトリにコピーされます。 アプリケーションが Windows ディレクトリに対してクエリを行う場合、rd セッションホストサーバーは、ユーザーのホームディレクトリの \Windows サブディレクトリを返します。
> - ログオンすると、リモートデスクトップサービスによって、コンピューター上の .ini ファイルよりもシステムの .ini ファイルが新しいかどうかがチェックされます。 システムのバージョンが新しい場合は、.ini ファイルが置き換えられるか、新しいバージョンにマージされます。 これは、この .ini ファイルに INISYNC ビット0x40 が設定されているかどうかによって異なります。 以前のバージョンの .ini ファイルは、Inifile という名前に変更されています。 **\ Terminal \ インストール**サブキーの下にあるシステムレジストリ値が**HKEY_CURrenT_USER**のバージョンより新しい場合は、サブキーのバージョンが削除され、 **\ terminal \ インストール**の新しいサブキーに置き換えられます。
>   ## <a name="BKMK_examples"></a>例
> - .Ini ファイルマッピングをホームディレクトリで無効にするには、次のように入力します。
>   ```
>   change user /install
>   ```
> - ホームディレクトリで .ini ファイルマッピングを有効にするには、次のように入力します。
>   ```
>   change user /execute
>   ```
> - .Ini ファイルマッピングの現在の設定を表示するには、次のように入力します。
>   ```
>   change user /query
>   ```
>   #### <a name="additional-references"></a>その他の参照情報
>   [コマンドライン構文のキー](command-line-syntax-key.md)
>   [変更](change.md)
>   [リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
