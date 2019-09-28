---
title: mstsc
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: bf813c75c83154c76d4aeb53a259495d4ad1369e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373347"
---
# <a name="mstsc"></a>mstsc

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバーまたはその他のリモートコンピューターへの接続を作成し、既存のリモートデスクトップ接続 (.rdp) 構成ファイルを編集して、クライアント接続マネージャーで作成された従来の接続ファイルを移行します。を新しい .rdp 接続ファイルに追加します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。

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
|   /v: < Server [: <Port>]   |                リモートコンピューターと、必要に応じて接続するポート番号を指定します。                 |
|         /admin          |                                   サーバーを管理するためのセッションに接続します。                                   |
|           /f            |                                    全画面表示モードでリモートデスクトップ接続を開始します。                                    |
|       /w: <Width>        |                                      リモートデスクトップウィンドウの幅を指定します。                                      |
|       /h: <Height>       |                                     リモートデスクトップウィンドウの高さを指定します。                                      |
|         /public         |                  リモートデスクトップをパブリックモードで実行します。 パブリックモードでは、パスワードとビットマップはキャッシュされません。                  |
|          /span          | リモートデスクトップの幅と高さをローカル仮想デスクトップと照合し、必要に応じて複数のモニターにまたがっています。 |
| /edit <Connection File> |                                         指定した .rdp ファイルを編集用に開きます。                                          |
|        /移行         |       クライアント接続マネージャーで作成された従来の接続ファイルを新しい .rdp 接続ファイルに移行します。       |
|           /?            |                                            コマンド プロンプトにヘルプを表示します。                                             |

## <a name="remarks"></a>コメント
-   既定の .rdp は、ユーザーごとに隠しファイルとしてユーザーの Documents フォルダーに格納されます。 ユーザーが作成した .rdp ファイルは、既定ではユーザーの Documents フォルダーに保存されますが、どこにでも保存できます。
-   複数のモニターにまたがる場合、モニターは同じ解像度を使用する必要があり、水平方向 (つまりサイドバイサイド) に調整する必要があります。 現在、クライアントシステム上で複数のモニターを垂直方向にまたがることはサポートされていません。

## <a name="BKMK_examples"></a>例
-   全画面表示モードでセッションに接続するには、次のように入力します。
    ```
    mstsc /f
    ```
-   編集するためにファイル名 .rdp という名前のファイルを開くには、次のように入力します。
    ```
    mstsc /edit filename.rdp
    ```

#### <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
