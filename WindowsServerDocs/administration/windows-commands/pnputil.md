---
title: pnputil
description: Pnputil ユーティリティを使用してドライバーストアを管理する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 134e6ce4b1fc44450047de3287b7daac67da4b6a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837515"
---
# <a name="pnputil"></a>pnputil

Pnputil は、ドライバーストアの管理に使用できるコマンドラインユーティリティです。 Pnputil を使用して、ドライバーパッケージの追加、ドライバーパッケージの削除、およびストア内のドライバーパッケージの一覧表示を行うことができます。

## <a name="syntax"></a>構文

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-a|識別された INF ファイルを追加することを指定します。|
|-d|特定された INF ファイルを削除することを指定します。|
|-e|すべてのサードパーティ製 INF ファイルを列挙するように指定します。|
|-f|特定された INF ファイルを強制的に削除するように指定します。 **– I**パラメーターと組み合わせて使用することはできません。|
|-i|識別された INF ファイルをインストールするように指定します。 は、 **-f**パラメーターと組み合わせて使用することはできません。|
|/?|コマンド プロンプトでヘルプを表示します。|


## <a name="examples"></a>例

-   pnputil-a a:\usbcam\USBCAM.INF は、USBCAM によって指定された INF ファイルを追加します。INF
-   svcutil.exe-c:\ ドライバー\*により、すべての INF ファイルが c:\ に追加されます。
-   pnputil-i-a a:\usbcam\USBCAM.INF は、指定されたドライバーを追加してインストールします。
-   pnputil – e は、すべてのサードパーティ製ドライバーを列挙します。
-   svcutil.exe-d oem0 は、指定されたを削除します。
-   svcutil.exe-f-d oem0 を指定すると、指定した INF ファイルが強制的に削除されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Popd](popd.md)