---
title: mstsc
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59801227-1e7e-4dbd-96e6-f54102a3ce92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5accd56ea622b85966bf0cb95750d8bb2d97e42
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839075"
---
# <a name="mstsc"></a>mstsc

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバーまたはその他のリモートコンピューターへの接続を作成し、既存のリモートデスクトップ接続 (.rdp) 構成ファイルを編集して、クライアント接続マネージャーで作成された従来の接続ファイルを新しい .rdp 接続ファイルに移行します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
mstsc.exe [<Connection File>] [/v:<Server>[:<Port>]] [/admin] [/f] [/w:<Width> /h:<Height>] [/public] [/span]
mstsc.exe /edit <Connection File>
mstsc.exe /migrate
```

### <a name="parameters"></a>パラメーター

|        パラメーター        |                                                         説明                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------|
|    <Connection File>    |                                   接続の .rdp ファイルの名前を指定します。                                    |
|  /v: < Server\>[: < ポート\>] |                リモートコンピューターと、必要に応じて接続するポート番号を指定します。                 |
|         /admin          |                                   サーバーを管理するためのセッションに接続します。                                   |
|           /f            |                                    全画面表示モードでリモートデスクトップ接続を開始します。                                    |
|       /w:<Width>        |                                      リモートデスクトップウィンドウの幅を指定します。                                      |
|       /h:<Height>       |                                     リモート デスクトップ ウィンドウの高さを指定します。                                      |
|         /public         |                  リモートデスクトップをパブリックモードで実行します。 パブリックモードでは、パスワードとビットマップはキャッシュされません。                  |
|          /span          | リモートデスクトップの幅と高さをローカル仮想デスクトップと照合し、必要に応じて複数のモニターにまたがっています。 |
| /edit <Connection File> |                                         指定した .rdp ファイルを編集用に開きます。                                          |
|        /migrate         |       クライアント接続マネージャーで作成された従来の接続ファイルを新しい .rdp 接続ファイルに移行します。       |
|           /?            |                                            コマンド プロンプトでヘルプを表示します。                                             |

## <a name="remarks"></a>コメント
-   既定の .rdp は、ユーザーごとに隠しファイルとしてユーザーの Documents フォルダーに格納されます。 ユーザーが作成した .rdp ファイルは、既定ではユーザーの Documents フォルダーに保存されますが、どこにでも保存できます。
-   複数のモニターにまたがる場合、モニターは同じ解像度を使用する必要があり、水平方向 (つまりサイドバイサイド) に調整する必要があります。 現在、クライアントシステム上で複数のモニターを垂直方向にまたがることはサポートされていません。

## <a name="examples"></a><a name=BKMK_examples></a>例
-   全画面表示モードでセッションに接続するには、次のように入力します。
    ```
    mstsc /f
    ```
-   編集するためにファイル名 .rdp という名前のファイルを開くには、次のように入力します。
    ```
    mstsc /edit filename.rdp
    ```

## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
