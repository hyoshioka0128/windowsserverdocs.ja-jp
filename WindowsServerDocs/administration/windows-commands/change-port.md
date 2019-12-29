---
title: change port
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e587572acd1af1cc7dbd2550e1eae5244d0d1dd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379597"
---
# <a name="change-port"></a>change port

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

MS-DOS アプリケーションと互換性があるように、COM ポートのマッピングを一覧表示または変更します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。
> ## <a name="syntax"></a>構文
> ```
> change port [<PortX>=<PortY> | /d <PortX> | /query]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |    パラメーター    |              説明               |
> |-----------------|----------------------------------------|
> | <PortX>=<PortY> |    COM <*PortX*>*を < の*> にマップします。    |
> |   /d <PortX>    | COM <*PortX*> のマッピングを削除します。 |
> |     /query      |  現在のポートマッピングが表示されます。   |
> |       /?        |  コマンド プロンプトにヘルプを表示します。  |
> 
> ## <a name="remarks"></a>コメント
> - ほとんどの MS-DOS アプリケーションは、COM1 ~ COM4 のシリアルポートのみをサポートしています。 **ポートの変更**コマンドは、シリアルポートを別のポート番号にマップします。これにより、高番号の COM ポートをサポートしていないアプリケーションでシリアルポートにアクセスできるようになります。 再マッピングは現在のセッションに対してのみ機能し、セッションからログオフして再度ログオンした場合は保持されません。
> - パラメーターを指定せずに**ポートを変更**して、使用可能な COM ポートとその現在のマッピングを表示します。
>   ## <a name="BKMK_examples"></a>例
> - MS-DOS ベースのアプリケーションで使用するために COM12 を COM1 にマップするには、次のように入力します。
>   ```
>   change port com12=com1
>   ```
> - 現在のポートマッピングを表示するには、次のように入力します。
>   ```
>   change port /query
>   ```
>   #### <a name="additional-references"></a>その他の参照情報
>   [コマンドライン構文のキー](command-line-syntax-key.md)
>   [変更](change.md)
>   [リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
