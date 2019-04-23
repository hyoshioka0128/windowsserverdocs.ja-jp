---
title: mmc
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bfa4030-ce42-40fb-922f-2f5145a80872
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 403f7569eaa2380d26cda805c40b1a623743952c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842013"
---
# <a name="mmc"></a>mmc

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Mmc のコマンド ライン オプションを使用して、特定を開くことができます**mmc**コンソールを開き、 **mmc**作成者モードで指定するか、32 ビットまたは 64 ビット バージョンの**mmc**が開かれます。
## <a name="syntax"></a>構文
```
mmc <path>\<filename>.msc [/a] [/64] [/32]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<path>\\<filename>.msc|開始**mmc**し保存したコンソールを開きます。 保存されているコンソール ファイルの完全なパスとファイル名を指定する必要があります。 コンソール ファイルを指定しない場合**mmc**新しいコンソールを開きます。|
|/a|作成者モードでは、保存されているコンソールを開きます。  保存されているコンソールに変更を加えるために使用します。|
|/64|64 ビット バージョンが開きます**mmc** (mmc64)。 Microsoft の 64 ビット オペレーティング システムを実行していて、64 ビットのスナップインを使用する場合にのみ、このオプションを使用します。|
|/32|32 ビット バージョンが開きます**mmc** (mmc32)。 Microsoft の 64 ビットのオペレーティング システムを実行するときに 32 ビット スナップインのみがある場合、このコマンド ライン オプションで開く mmc で 32 ビットのスナップインを実行できます。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   使用して、 <path>**\\**<filename>**.msc** コマンド ライン オプションをコマンドラインまたはコンソール ファイルの格納場所を明示的に依存しないショートカットを作成する環境変数を使用することができます。 たとえばかどうか、コンソール ファイルへのパスがシステム フォルダーには (たとえば、 **mmc c:\winnt\system32\console_name.msc**)、拡張可能なデータ文字列を使用することができます **%systemroot%** 場所を指定 (**mmc%systemroot%\system32\console_name.msc**)。 別のコンピューターで作業している組織内のユーザーにタスクを委任する場合に便利ですがあります。
-   使用して、 **/a** コマンド ライン オプション コンソールがこのオプションで開かれると、既定のモードに関係なく、作成者モードで開きます。 これは完全に変わりませんファイルの既定のモード設定このオプションを省略すると、mmc は、既定のモード設定に従ってコンソール ファイルを開きます。
-   開いた後**mmc**またはコンソール ファイル作成者モードでは、クリックして、既存のコンソールを開くことができます**開く**上、**コンソール**メニュー。
-   コマンドラインを使用して開くのためのショートカットを作成することができます**mmc**コンソールを保存します。 コマンド ライン コマンドは、**実行**コマンドを**開始**] メニューの [任意のコマンド プロンプト ウィンドウで、ショートカット、またはバッチ ファイルまたはコマンドを呼び出すプログラムにします。
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)

