---
title: tsprof
description: Tsprof の Windows コマンドに関するトピックでは、リモートデスクトップサービスユーザー構成情報をあるユーザーから別のユーザーにコピーします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 27047868-b706-4208-b7e0-1437a2325dd3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3b1037b6daff467a71517917d423e4cbe87a97f2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832475"
---
# <a name="tsprof"></a>tsprof

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

1 人のユーザーから別のリモート デスクトップ サービス ユーザーの構成情報をコピーします。
リモートデスクトップサービスユーザーの構成情報は、[ローカルユーザーとグループ]、[active directory ユーザーとコンピューター] のリモートデスクトップサービスの拡張機能に表示されます。

**tsprof**では、ユーザーのプロファイルパスを設定することもできます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
tsprof /update {/domain:<DomainName> | /local} /profile:<path> <UserName>
tsprof /copy {/domain:<DomainName> | /local} [/profile:<path>] <Src_usr> <Dest_usr>
tsprof /q {/domain:<DomainName> | /local} <UserName>
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/update|ドメイン <*DomainName*> 内の <*ユーザー名*> のプロファイルパス情報を <*Profilepath*> に更新します。|
|/domain:\<DomainName >|操作が適用されるドメインの名前を指定します。|
|/local|ローカルユーザーアカウントにのみ操作を適用します。|
|/profile:\<パス >|[ローカルユーザーとグループ]、[active directory ユーザーとコンピューター] のリモートデスクトップサービス拡張機能に表示されるプロファイルパスを指定します。|
|\<ユーザー名 >|サーバープロファイルパスを更新または照会するユーザーの名前を指定します。|
|/copy|ユーザー構成情報を \<*sourceuser*> から \<*destinationuser*> にコピーし、\<*destinationuser*> のプロファイルパス情報を \<*Profilepath*> に更新します。 \<*sourceuser*> と \<*destinationuser*> は両方ともローカルであるか、ドメイン \<*DomainName*> に存在する必要があります。|
|\<Src_usr >|ユーザー構成情報をコピーするユーザーの名前を指定します。|
|\<Dest_usr >|ユーザー構成情報をコピーするユーザーの名前を指定します。|
|/q|サーバープロファイルパスに対してクエリを実行するユーザーの現在のプロファイルパスを表示します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント
-   **Tsprof**コマンドを使用できるのは、windows server 2008 を実行しているコンピューターにターミナルサーバーの役割サービスをインストールした場合、または windows Server 2008 R2 を実行しているコンピューターに RD セッションホスト役割サービスをインストールした場合のみです。

## <a name="examples"></a><a name=BKMK_examples></a>例
-   ユーザー構成情報を LocalUser1 から LocalUser2 にコピーするには、次のように入力します。
    ```
    tsprof /copy /local LocalUser1 LocalUser2
    ```
-   LocalUser1 のリモートデスクトップサービスプロファイルパスを c:\ プロファイルという名前のディレクトリに設定するには、次のように入力します。
    ```
    tsprof /update /local /profile:c:\profiles LocalUser1
    ```

## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
