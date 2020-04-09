---
title: bitsadmin setdisplayname
description: Bitsadmin setdisplayname の Windows コマンドに関するトピックでは、指定されたジョブの表示名を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 601c5b406132e70fb7d4facb97329f7456002bb4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849545"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

指定されたジョブの表示名を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|DisplayName|指定されたジョブの表示名に使用されるテキスト。|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの表示名を*myDownloadJob2*に設定します。
```
C:\>bitsadmin /SetDisplayName myDownloadJob Download Music Job
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)