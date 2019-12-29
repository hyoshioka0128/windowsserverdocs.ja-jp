---
title: pnputil
description: Pnputil ユーティリティを使用してドライバーストアを管理する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f20c60bfd9ae33497dd356c7797b9fb1d2b51d18
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372288"
---
# <a name="pnputil"></a>pnputil

Pnputil は、ドライバーストアの管理に使用できるコマンドラインユーティリティです。 Pnputil を使用して、ドライバーパッケージの追加、ドライバーパッケージの削除、およびストア内のドライバーパッケージの一覧表示を行うことができます。

## <a name="syntax"></a>構文

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-a|識別された INF ファイルを追加することを指定します。|
|-d|特定された INF ファイルを削除することを指定します。|
|-e|すべてのサードパーティ製 INF ファイルを列挙するように指定します。|
|-f|特定された INF ファイルを強制的に削除するように指定します。 **– I**パラメーターと組み合わせて使用することはできません。|
|-i|識別された INF ファイルをインストールするように指定します。 は、 **-f**パラメーターと組み合わせて使用することはできません。|
|/?|コマンド プロンプトにヘルプを表示します。|


## <a name="examples"></a>使用例

-   pnputil-a a:\usbcam\USBCAM.INF は、USBCAM によって指定された INF ファイルを追加します。INF
-   svcutil.exe-a c:\ drivers\*.inf にすべての INF ファイルが追加されます。
-   pnputil-i-a a:\usbcam\USBCAM.INF は、指定されたドライバーを追加してインストールします。
-   pnputil – e は、すべてのサードパーティ製ドライバーを列挙します。
-   svcutil.exe-d oem0 は、指定されたを削除します。
-   svcutil.exe-f-d oem0 を指定すると、指定した INF ファイルが強制的に削除されます。

## <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Popd](popd.md)