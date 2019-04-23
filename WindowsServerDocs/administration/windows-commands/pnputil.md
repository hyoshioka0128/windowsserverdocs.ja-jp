---
title: pnputil
description: Pnputil.exe ユーティリティを使用したドライバー ストアを管理する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5bde78d97be8def9f8594572869c34ef213db480
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862543"
---
# <a name="pnputil"></a>pnputil

Pnputil.exe とは、ドライバー ストアの管理に使用できるコマンド ライン ユーティリティです。 Pnputil を使用して、ドライバー パッケージを追加、ドライバー パッケージ、および、ストア内にある一覧のドライバー パッケージを削除することができます。

## <a name="syntax"></a>構文

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-a|指定した INF ファイルを追加することを指定します。|
|-d|指定した INF ファイルを削除することを指定します。|
|-e|すべてのサード パーティ製の INF ファイルを列挙することを指定します。|
|-f|強制的に指定した INF ファイルの削除を指定します。 組み合わせて使用することはできません、 **– i**パラメーター。|
|-i|指定した INF ファイルをインストールすることを指定します。 組み合わせて使用することはできません、 **-f**パラメーター。|
|/?|コマンド プロンプトにヘルプを表示します。|


## <a name="examples"></a>例

-   pnputil.exe-a:\usbcam\USBCAM します。INF は、USBCAM によって指定される INF ファイルを追加します。INF
-   pnputil.exe -a c:\drivers\*.inf  Adds all INF files in c:\drivers\
-   pnputil.exe-i-a:\usbcam\USBCAM します。INF を追加し、指定されたドライバーをインストールします。
-   pnputil.exe – e では、すべてのサード パーティ製ドライバーを列挙します。
-   指定した pnputil.exe-d oem0.inf を削除します。
-   pnputil.exe-f-d oem0.inf では、指定した INF ファイルの削除を強制します。

## <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[popd](popd.md)