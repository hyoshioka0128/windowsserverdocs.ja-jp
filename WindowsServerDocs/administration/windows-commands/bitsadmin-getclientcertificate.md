---
title: bitsadmin getclientcertificate
description: Bitsadmin getclientcertificate コマンドの参照記事で、ジョブからクライアント証明書を取得します。
ms.topic: article
ms.assetid: 4fc8f408-085e-43a0-9fa8-3d798ef107b1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3deb42c0b29f238bfd0a3b0fddbea14833d38b4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894507"
---
# <a name="bitsadmin-getclientcertificate"></a>bitsadmin getclientcertificate

ジョブからクライアント証明書を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getclientcertificate <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのクライアント証明書を取得するには、次のようにします。

```
bitsadmin /getclientcertificate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
