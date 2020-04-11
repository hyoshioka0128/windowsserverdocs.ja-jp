---
title: bitsadmin setsecurityflags
description: '**Bitsadmin setsecurityflags**の Windows コマンドトピックでは、http のセキュリティフラグを設定して、BITS が証明書失効リストを確認し、特定の証明書エラーを無視し、サーバーが HTTP 要求をリダイレクトするときに使用するポリシーを定義するかどうかを決定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d73361bceda8c0eb24992bdee176b47bf82a878
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122728"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags

HTTP のセキュリティフラグを設定して、BITS が証明書失効リストを確認し、特定の証明書エラーを無視し、サーバーが HTTP 要求をリダイレクトするときに使用するポリシーを定義するかどうかを決定します。 値は符号なし整数です。

## <a name="syntax"></a>構文

```
bitsadmin /setsecurityflags <job> <value>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| value | には、次のような通知フラグを1つ以上含めることができます。<ul><li>CRL チェックを有効にするには、最下位ビットを設定します。</li><li>サーバー証明書の不適切な共通名を無視するには、右側の2番目のビットを設定します。</li><li>サーバー証明書の誤った日付を無視するには、右側の3番目のビットを設定します。</li><li>サーバー証明書の正しくない証明機関を無視するには、右側の4番目のビットを設定します。</li><li>サーバー証明書の不適切な使用を無視するには、右側の5番目のビットを設定します。</li><li>指定したリダイレクトポリシーを実装するには、次のように、右側の11番目のビットを使用します。<ul><li>**0、0、0。** リダイレクトは自動的に許可されます。</li><li>**0、0、1。** **IBackgroundCopyFile**インターフェイスのリモート名は、リダイレクトが発生した場合に更新されます。</li><li>**0、1、0。** リダイレクトが発生した場合、BITS はジョブを失敗させる。</li></ul></li><li>HTTPS から HTTP へのリダイレクトを許可するには、右側の12番目のビットを設定します。</li></ul> |

## <a name="examples"></a>例

次の例では、セキュリティフラグを設定して、 *Mydownloadjob*という名前のジョブの CRL チェックを有効にします。

```
C:\>bitsadmin /setsecurityflags myDownloadJob 0x0001
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)