---
title: bitsadmin setproxysettings
description: Bitsadmin setproxysettings コマンドの参照記事。指定されたジョブのプロキシ設定を設定します。
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fb4e8893aa4becac49e5837baef3148541136ff
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892970"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings

指定されたジョブのプロキシ設定を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setproxysettings <job> <usage> [list] [bypass]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| usage | プロキシの使用方法を設定します。次に例を示します。<ul><li>**PRECONFIG.** 所有者の Internet Explorer の既定値を使用します。</li><li>**NO_PROXY。** プロキシサーバーは使用しないでください。</li><li>**オーバーライド.** 明示的なプロキシリストとバイパスリストを使用します。 プロキシの一覧とプロキシのバイパス情報は、の後に続く必要があります。</li><li>**認識.** プロキシ設定を自動的に検出します。</li></ul> |
| list | *Usage*パラメーターが OVERRIDE に設定されている場合に使用します。 使用するプロキシサーバーのコンマ区切りの一覧が含まれている必要があります。 |
| バイパス | *Usage*パラメーターが OVERRIDE に設定されている場合に使用します。 ホスト名または IP アドレスのスペース区切りの一覧、またはその両方を含める必要があります。この場合、転送はプロキシ経由でルーティングされません。 これは `<local>` 、同じ LAN 上のすべてのサーバーを参照することができます。 空のプロキシバイパスリストには NULL 値を使用できます。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのさまざまな使用方法を使用してプロキシ設定を設定するには、次のようにします。

```
bitsadmin /setproxysettings myDownloadJob PRECONFIG
```

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
```
```
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80
```

```
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
