---
title: bitsadmin takeownership
description: 管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにする bitsadmin を取得するための Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ea0ce7cb-440a-498f-a3ef-8368fa43e399
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a2c0bfc1fcb1606102aece76129c49aad701ead
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849025"
---
# <a name="bitsadmin-takeownership"></a>bitsadmin takeownership

管理者特権を持つユーザーが、指定されたジョブの所有権を取得できるようにします。

## <a name="syntax"></a>構文

```
bitsadmin /TakeOwnership <Job>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの所有権を取得します。
```
C:\>bitsadmin /TakeOwnership myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)