---
title: tsprof
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27047868-b706-4208-b7e0-1437a2325dd3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e17d60126125fcd4b10373133dd61ca0db030290
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836073"
---
# <a name="tsprof"></a>tsprof

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1 人のユーザーから別のリモート デスクトップ サービス ユーザーの構成情報をコピーします。
リモート デスクトップ サービス ユーザーの構成情報は、リモート デスクトップ サービスの拡張機能をローカル ユーザーとグループと active directory ユーザーとコンピューターに表示されます。

**tsprof**ユーザーのプロファイル パスを設定することもできます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)、を参照してください。

## <a name="syntax"></a>構文
```
tsprof /update {/domain:<DomainName> | /local} /profile:<path> <UserName>
tsprof /copy {/domain:<DomainName> | /local} [/profile:<path>] <Src_usr> <Dest_usr>
tsprof /q {/domain:<DomainName> | /local} <UserName>
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/update|プロファイル パス情報を更新 <*UserName*> ドメイン <*DomainName*> を <*%profilepath%*>。|
|/domain:\<DomainName >|操作を適用するドメインの名前を指定します。|
|/local|ローカル ユーザー アカウントのみに適用します。|
|/profile:\<パス >|リモート デスクトップ サービスの拡張機能では、ローカル ユーザーとグループと active directory ユーザーとコンピューター で表示されるプロファイルのパスを指定します。|
|\<ユーザー名 >|更新またはサーバー プロファイル パスを照会するユーザーの名前を指定します。|
|/copy|ユーザーの構成情報をコピー \< *SourceUser*> に\< *DestinationUser*> のプロファイル パス情報を更新および\< *DestinationUser*> に\< *%profilepath%*>。 両方\< *SourceUser*> と\< *DestinationUser*> か、ローカルであるか、ドメインになければなりません\< *DomainName*>.|
|\<Src_usr>|ユーザーの構成情報をコピーするユーザーの名前を指定します。|
|\<Dest_usr >|ユーザーの構成情報をコピーするユーザーの名前を指定します。|
|/q|サーバーのプロファイル パスをクエリするユーザーの現在のプロファイル パスを表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   **Tsprof**コマンドは Windows Server 2008 R2 を実行するコンピューターで Windows Server 2008 または RD セッション ホスト役割サービスを実行するコンピューターにターミナル サーバーの役割サービスをインストールしたときにのみ使用できます。

## <a name="BKMK_examples"></a>例
-   ユーザーの構成情報を LocalUser1 から LocalUser2 にコピーするには、次のように入力します。
    ```
    tsprof /copy /local LocalUser1 LocalUser2
    ```
-   "C:\profiles"という名前のディレクトリに LocalUser1 のリモート デスクトップ サービスのプロファイル パスを設定するには、次のように入力します。
    ```
    tsprof /update /local /profile:c:\profiles LocalUser1
    ```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](command-line-syntax-key.md)
[リモート デスクトップ サービス &#40;ターミナル サービス&#41; コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
