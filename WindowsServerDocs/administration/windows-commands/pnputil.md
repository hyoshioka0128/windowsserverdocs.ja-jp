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
ms.openlocfilehash: 4c6bcb138e8bd7308c01c2c53fba83b69362298a
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436367"
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
|-E|すべてのサードパーティ製 INF ファイルを列挙するように指定します。|
|-f|特定された INF ファイルを強制的に削除するように指定します。 **– I**パラメーターと組み合わせて使用することはできません。|
|-i|識別された INF ファイルをインストールするように指定します。 は、 **-f**パラメーターと組み合わせて使用することはできません。|
|/?|コマンド プロンプトにヘルプを表示します。|


## <a name="examples"></a>例

-   pnputil-a a:\usbcam\USBCAM.INF は、USBCAM によって指定された INF ファイルを追加します。INF
-   svcutil.exe-c:\ ドライバー \* 。 inf によってすべての inf ファイルが追加されます。
-   pnputil-i-a a:\usbcam\USBCAM.INF は、指定されたドライバーを追加してインストールします。
-   pnputil – e は、すべてのサードパーティ製ドライバーを列挙します。
-   svcutil.exe-d oem0 は、指定されたを削除します。
-   svcutil.exe-f-d oem0 を指定すると、指定した INF ファイルが強制的に削除されます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Popd](popd.md)