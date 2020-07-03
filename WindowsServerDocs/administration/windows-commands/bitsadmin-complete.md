---
title: bitsadmin complete
description: ジョブを完了する bitsadmin complete コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08fb74690f5a8f70611bb6ca52a291bec89d81e8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928351"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

ジョブを完了します。 ジョブが転送済み状態に移行した後に、このスイッチを使用します。 そうしないと、正常に転送されたファイルのみが使用可能になります。

## <a name="syntax"></a>構文

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="example"></a>例

*Mydownloadjob*ジョブを完了するには、次のようにし `TRANSFERRED` ます。

```
bitsadmin /complete myDownloadJob
```

複数のジョブが*Mydownloadjob*を名前として使用している場合は、ジョブの GUID を使用して、ジョブの完了を一意に識別する必要があります。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
