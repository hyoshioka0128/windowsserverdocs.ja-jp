---
title: change port
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 477761c35f08d5ec81adae80ba8f2fe9667786e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818643"
---
# <a name="change-port"></a>change port

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リストまたは MS-DOS アプリケーションと互換性がある COM ポートのマッピングを変更します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
## <a name="syntax"></a>構文
```
change port [<PortX>=<PortY> | /d <PortX> | /query]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<PortX>=<PortY>|COM マップ <*マッピング*> を <*PortY*>。|
|/d <PortX>|COM のマッピングを削除します <*マッピング*>。|
|/query|現在のポート マッピングを表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   ほとんどの MS-DOS アプリケーションは、COM4 シリアル ポート経由の COM1 のみをサポートします。 **ポートを変更**コマンドは、大きい番号の COM をサポートしていないアプリケーション、シリアル ポートにアクセスするポートを許可する、別のポート番号をシリアル ポートをマップします。 再マップでは、現在のセッションでのみ機能し、セッションからログオフし、もう一度ログオンする場合は保持されません。
-   使用**ポートを変更**利用可能な COM ポートとその現在のマッピングを表示するパラメーターなし。
## <a name="BKMK_examples"></a>例
-   Ms-dos アプリケーションを使用するための COM1 に COM12 をマップして、次のように入力します。
    ```
    change port com12=com1
    ```
-   現在のポート マッピングを表示するには、次のように入力します。
    ```
    change port /query
    ```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[変更](change.md)
[Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
