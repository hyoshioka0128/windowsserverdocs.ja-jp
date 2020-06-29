---
title: pnputil
description: pnputil.exe ユーティリティを使用して、ドライバーパッケージの追加、ドライバーパッケージの削除、およびドライバーストア内のドライバーパッケージの一覧表示を行う、pnputil コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fab686b8-09d3-4f6c-afa2-630e6036f44c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6484a3e55c6e5f3b4cb51119ead5cb488dca0721
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472401"
---
# <a name="pnputil"></a>pnputil

Pnputil.exe は、ドライバーストアの管理に使用できるコマンドラインユーティリティです。 このコマンドを使用して、ドライバーパッケージの追加、ドライバーパッケージの削除、およびストア内のドライバーパッケージの一覧表示を行うことができます。

## <a name="syntax"></a>構文

```
pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -a | 識別された INF ファイルを追加することを指定します。 |
| -d | 特定された INF ファイルを削除することを指定します。 |
| -E | すべてのサードパーティ製 INF ファイルを列挙するように指定します。 |
| -f | 特定された INF ファイルを強制的に削除するように指定します。 **– I**パラメーターと共に使用することはできません。 |
| -i | 識別された INF ファイルをインストールするように指定します。 は、 **-f**パラメーターと組み合わせて使用することはできません。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

USBCAM という名前の INF ファイルを追加します。INF、次のように入力します。

```
pnputil.exe -a a:\usbcam\USBCAM.INF
```

C:\ ドライバーにあるすべての INF ファイルを追加するには、次のように入力します。

```
pnputil.exe -a c:\drivers\*.inf
```

USBCAM を追加してインストールします。INF ドライバー、次のように入力します。

```
pnputil.exe -i -a a:\usbcam\USBCAM.INF
```

すべてのサードパーティドライバーを列挙するには、次のように入力します。

```
pnputil.exe –e
```

Oem0 という名前の INF ファイルとドライバーを削除するには、次のように入力します。

```
pnputil.exe -d oem0.inf
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [popd コマンド](popd.md)
