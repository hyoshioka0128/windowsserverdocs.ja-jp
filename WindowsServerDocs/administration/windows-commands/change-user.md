---
title: change user
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: bedef9f996554a3b5745b47f646204646fdfa9a6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434414"
---
# <a name="change-user"></a>change user

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーのインストール モードを変更します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
> ## <a name="syntax"></a>構文
> ```
> change user {/execute | /install | /query}
> ```
> ## <a name="parameters"></a>パラメーター
> 
> | パラメーター |                                                                                                 説明                                                                                                  |
> |-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | /実行  |                                                                ホーム ディレクトリに .ini ファイルのマッピングを有効にします。 これは、既定の設定です。                                                                 |
> | /install  | ホーム ディレクトリに .ini ファイルのマッピングを無効にします。 すべての .ini ファイルは読み取りし、システム ディレクトリに書き込まれます。 Rd セッション ホスト サーバーにアプリケーションをインストールする場合は、.ini ファイルのマッピングを無効にする必要があります。 |
> |  /query   |                                                                             .Ini ファイルのマッピングの現在の設定を表示します。                                                                              |
> |    /?     |                                                                                     コマンド プロンプトにヘルプを表示します。                                                                                     |
> 
> ## <a name="remarks"></a>注釈
> - 使用 **「change user/install**システム ディレクトリで、アプリケーションの .ini ファイルを作成するアプリケーションをインストールする前にします。 これらのファイルは、ユーザー固有の .ini ファイルが作成されたときに、ソースとして使用されます。 アプリケーションをインストールすると、次のように使用します。 **change user**標準の .ini ファイルのマッピングに戻す。
> - 初めてのアプリケーションを実行する、.ini ファイルのホーム ディレクトリを検索します。 .Ini ファイルにホーム ディレクトリに存在しないシステムのディレクトリ内にある場合は、リモート デスクトップ サービス、.ini ファイルにコピー ホーム ディレクトリでは、各ユーザーがアプリケーションの .ini ファイルの一意のコピーを持っていることを確認します。 新しい .ini ファイルは、ホーム ディレクトリに作成されます。
> - 各ユーザー、アプリケーション用の .ini ファイルの一意のコピーが必要です。 これにより、別のユーザーが互換性のないアプリケーションの構成 (たとえば、異なる既定のディレクトリまたは画面解像度) を持つ可能性があります。
> - システムがインストール モードの場合 (つまり、 **「change user/install**)、いくつか問題が発生します。 作成されたすべてのレジストリ エントリが影付き**hkey_local_machine \software\microsoft\windows NT\Currentversion\Terminal Server\Install**、いずれかで、 **\SOFTWARE**サブキーまたは、 **\MACHINE**サブキー。 サブキーが追加された**HKEY_CURrenT_USER**下にコピーされます、 **\SOFTWARE**サブキー、およびサブキーに追加**HKEY_LOCAL_MACHINE**下にコピーされます、 **\マシン**サブキー。 アプリケーションでは、Windows ディレクトリを照会 GetWindowsdirectory などのシステム呼び出しを使用して、rd セッション ホスト サーバーは、systemroot ディレクトリを返します。 WritePrivateProfileString などのシステム呼び出しを使用して、.ini ファイルのエントリが追加された場合は、systemroot ディレクトリの下の .ini ファイルに追加されます。
> - システムが実行モードに返されるときに (つまり、**ユーザーを変更する/実行**)、アプリケーションの下のレジストリ エントリを読み込もうと**HKEY_CURrenT_USER**存在しない、リモート デスクトップ サービスキーのコピーが存在するかどうかを確認するためのチェック、 **\Terminal Server\Install**サブキー。 下の適切な場所にサブキーをコピーする場合は、 **HKEY_CURrenT_USER**します。 アプリケーションが存在しない .ini ファイルから読み取るしようとすると、リモート デスクトップ サービスはシステム ルートの下には、その .ini ファイルを検索します。 .Ini ファイルがシステム ルートにある場合は、ユーザーのホーム ディレクトリの \Windows サブディレクトリにコピーされます。 アプリケーションでは、Windows ディレクトリを照会、rd セッション ホスト サーバーはユーザーのホーム ディレクトリの \Windows サブディレクトリを返します。
> - ログオン時にリモート デスクトップ サービスは、そのシステムの .ini ファイルがコンピューターに、.ini ファイルより新しいかどうかを確認します。 .Ini ファイルは、システムのバージョンが新しい場合は、交換か、新しいバージョンとマージします。 これは、この .ini ファイルの設定は、かどうか、INISYNC ビット、0x40 によって異なります。 以前のバージョンの .ini ファイル Inifile.ctx 名前が付けられます。 下に、システム レジストリ値の場合、 **\Terminal Server\Install**サブキーの下で、バージョンより新しいは**HKEY_CURrenT_USER**サブキーのバージョンが削除され、新しいサブキーに置き換えられます **\Terminal Server\Install**します。
>   ## <a name="BKMK_examples"></a>例
> - ホーム ディレクトリで .ini ファイルのマッピングを無効にするには、次のように入力します。
>   ```
>   change user /install
>   ```
> - ホーム ディレクトリで .ini ファイルのマッピングを有効にするには、次のように入力します。
>   ```
>   change user /execute
>   ```
> - .Ini ファイルのマッピングの現在の設定を表示するには、次のように入力します。
>   ```
>   change user /query
>   ```
>   #### <a name="additional-references"></a>その他の参照
>   [コマンドライン構文のポイント](command-line-syntax-key.md)
>   [変更](change.md)
>   [Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
