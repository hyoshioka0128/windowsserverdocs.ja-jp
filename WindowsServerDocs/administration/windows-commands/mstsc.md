---
title: mstsc
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b6f89c1e3b0d36f14dbd55f9e6994c788305b30d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437186"
---
# <a name="mstsc"></a>mstsc

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーまたは他のリモート コンピューターへの接続を作成し、既存のリモート デスクトップ接続 (.rdp) 構成ファイルを編集し、クライアント接続マネージャーで作成されたレガシ接続ファイルの移行新しい .rdp 接続ファイル。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
mstsc.exe [<Connection File>] [/v:<Server>[:<Port>]] [/admin] [/f] [/w:<Width> /h:<Height>] [/public] [/span]
mstsc.exe /edit <Connection File>
mstsc.exe /migrate
```

## <a name="parameters"></a>パラメーター

|        パラメーター        |                                                         説明                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|    <Connection File>    |                                   接続の .rdp ファイルの名前を指定します。                                    |
|   /v: < サーバー [:<Port>]   |                リモート コンピューターと、必要に応じて、接続するポート番号を指定します。                 |
|         /admin          |                                   サーバーを管理するためのセッションに接続します。                                   |
|           /f            |                                    全画面表示モードでリモート デスクトップ接続を開始します。                                    |
|       /w:<Width>        |                                      リモート デスクトップ ウィンドウの幅を指定します。                                      |
|       /h:<Height>       |                                     リモート デスクトップ ウィンドウの高さを指定します。                                      |
|         パブリック/         |                  パブリック モードでリモート デスクトップを実行します。 パブリック モードでのパスワードとビットマップはキャッシュされません。                  |
|          /span          | リモート デスクトップの幅と高さを必要に応じて、複数のモニターにまたがる、ローカル仮想デスクトップに一致します。 |
| /edit <Connection File> |                                         編集するための指定した .rdp ファイルを開きます。                                          |
|        /移行         |       クライアントとの接続マネージャーを新しい .rdp 接続ファイルに作成されたレガシ接続ファイルを移行します。       |
|           /?            |                                            コマンド プロンプトにヘルプを表示します。                                             |

## <a name="remarks"></a>注釈
-   Default.rdp は、各ユーザーのユーザーの Documents フォルダー内の非表示ファイルとして格納されます。 .Rdp ファイルを作成したユーザーは、既定では、ユーザーの Documents フォルダーに保存されますが、任意の場所に保存することができます。
-   複数のモニター、モニターは、同じ解像度を使用する必要があり、横方向に配置する必要があります (つまり、並行して)。 現在、クライアント システム上の垂直方向に複数のモニターにまたがるようにサポートされていません。

## <a name="BKMK_examples"></a>例
-   全画面表示モードでのセッションに接続するに次のように入力します。
    ```
    mstsc /f
    ```
-   編集用 filename.rdp をという名前のファイルを開くには、次のように入力します。
    ```
    mstsc /edit filename.rdp
    ```

#### <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [リモート デスクトップ サービス&#40;ターミナル サービス&#41;コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
