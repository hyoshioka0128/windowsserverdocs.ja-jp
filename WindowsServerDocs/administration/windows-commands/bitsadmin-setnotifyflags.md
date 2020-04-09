---
title: bitsadmin setnotifyflags
description: Bitsadmin setnotifyflags の Windows コマンドに関するトピックでは、指定したジョブのイベント通知フラグを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5763d95-94a6-45ca-9e03-891c20047e06
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd3001fa4ae7f51cab92556f4f2f498511cca5ae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849285"
---
# <a name="bitsadmin-setnotifyflags"></a>bitsadmin setnotifyflags

指定されたジョブのイベント通知フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetNotifyFlags <Job> <NotifyFlags>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|NotifyFlags|「解説」を参照|

## <a name="remarks"></a>コメント

**Notifyflags**パラメーターには、次の通知フラグを1つ以上含めることができます。

|-----|-----| | 1 |ジョブ内のすべてのファイルが転送されたときにイベントを生成します |。| 2 |エラーが発生したときにイベントを生成します |。| 4 |通知を無効にします |。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブについて、転送された通知フラグとエラーイベントジョブを設定します。
```
C:\>bitsadmin /SetNotifyFlags myDownloadJob 3
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)