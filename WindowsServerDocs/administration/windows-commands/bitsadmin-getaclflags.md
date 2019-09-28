---
title: bitsadmin getaclflags
description: '**Bitsadmin getaclflags**の Windows コマンドトピックでは、アクセス制御リストの伝達フラグを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad98cd742161ae06be5cba7acde7b810eaf199d6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381789"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

アクセス制御リスト (ACL) の伝達フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetAclFlags <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

次のフラグ値の1つまたは複数を表示します。
-   O:所有者情報をファイルと共にコピーします。
-   G:グループ情報をファイルと共にコピーします。
-   D:DACL 情報をファイルと共にコピーします。
-   送信:ファイルを使用して SACL 情報をコピーします。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアクセス制御リストの伝達フラグを取得します。
```
C:\>bitsadmin /getaclflags myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)