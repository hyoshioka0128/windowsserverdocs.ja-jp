---
title: bitsadmin setnoprogresstimeout
description: '**Bitsadmin setnoprogresstimeout**の Windows コマンドに関するトピックでは、一時的なエラーが発生した後にサービスがファイルの転送を試行する時間の長さを秒単位で設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 761d0d76a2c70af9d4ad68aa564c1a9816691d0d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380500"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

最初の一時的なエラーが発生した後に、BITS がファイルの転送を試行する時間を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetNoProgressTimeout <Job> <TimeOutvalue>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|TimeOutvalue|秒単位で表された数値。|

## <a name="remarks"></a>コメント

-   ジョブで一時的なエラーが発生した場合、進行状況のタイムアウト間隔は開始されません。
-   データのバイトが正常に転送されると、タイムアウト間隔が停止またはリセットされます。
-   進行状況のタイムアウト間隔が*TimeOutvalue*を超えると、ジョブは致命的なエラー状態になります。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの 進行状況なしのタイムアウト値を20秒に設定します。
```
C:\>bitsadmin /SetNoProgressTimeout myDownloadJob 20
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)