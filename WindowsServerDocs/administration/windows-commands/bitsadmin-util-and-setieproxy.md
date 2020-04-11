---
title: bitsadmin util と setieproxy
description: '**Bitsadmin util と setieproxy**の Windows コマンドに関するトピックでは、サービスアカウントを使用してファイルを転送するときに使用するプロキシ設定を設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ebb33ff917ddd43bbc62413755ca28478ad5a95
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122529"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util と setieproxy

サービスアカウントを使用してファイルを転送するときに使用するプロキシ設定を設定します。 このコマンドを正常に完了するには、管理者特権のコマンドプロンプトから実行する必要があります。

> [!NOTE]
> このコマンドは、BITS 1.5 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /util /setieproxy <account> <usage> [/conn <connectionname>]
```

### <a name="parameters"></a>パラメーター


| パラメーター | 説明 |
| --------- | ---------- |
| アカウント | プロキシ設定を定義するサービスアカウントを指定します。 表示される値は次のとおりです。<ul><li>LOCALSYSTEM</li><li>   NETWORKSERVICE</li><li>LOCALSERVICE.</li></ul> |
| [使用状況] | 使用するプロキシ検出の形式を指定します。 表示される値は次のとおりです。<ul><li>**NO_PROXY。** プロキシサーバーは使用しないでください。</li><li>**認識.** プロキシ設定を自動的に検出します。</li><li>**MANUAL_PROXY。** 指定されたプロキシリストとバイパスリストを使用します。 使用状況タグの直後にリストを指定する必要があります。 たとえば、`MANUAL_PROXY proxy1,proxy2 NULL` と記述します。<ul><li>**プロキシの一覧。** 使用するプロキシサーバーのコンマ区切りの一覧。</li><li>**バイパスリスト。** 転送がプロキシ経由でルーティングされない、ホスト名または IP アドレス、またはその両方のスペース区切りのリスト。 これは、同じ LAN 上のすべてのサーバーを参照するローカル > \<できます。 NULL またはの値は、空のプロキシバイパスリストに使用できます。</li></ul><li>**AUTOSCRIPT。** **自動検出**と同じです。ただし、スクリプトも実行されます。 使用状況タグの直後にスクリプト URL を指定する必要があります。 たとえば、`AUTOSCRIPT http://server/proxy.js` と記述します。</li><li>**解除.** **NO_PROXY**と同じですが、手動プロキシ url (指定されている場合) および自動検出を使用して検出されたすべての url が削除される点が異なります。</li></ul> |
| connectionname | 省略可。 **/Conn**パラメーターと共に使用して、使用するモデム接続を指定します。 **/Conn**パラメーターを指定しない場合、BITS は LAN 接続を使用します。 |

## <a name="remarks"></a>コメント

このスイッチを使用する後続の各呼び出しは、以前に指定された使用量を置き換えますが、以前に定義された使用法のパラメーターは置き換えられません。 たとえば、個別の呼び出しで**NO_PROXY**、**自動検出**、および**MANUAL_PROXY**を指定した場合、BITS は最後に指定された使用量を使用しますが、以前に定義した使用法のパラメーターを保持します。

## <a name="examples"></a>例

次の例では、ネットワークサービスアカウントのプロキシ使用法を設定します。

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

その他の例を次に示します。

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
```

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)