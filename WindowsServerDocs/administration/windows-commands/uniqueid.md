---
title: uniqueid
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64f097766daa4c87ec84f42dd53f49792a160bb9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363909"
---
# <a name="uniqueid"></a>uniqueid



フォーカスがあるディスクの GUID パーティションテーブル (GPT) 識別子またはマスターブートレコード (MBR) 署名を表示または設定します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

## <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                                             説明                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id = {\<dword > |                                                                                               <GUID>}                                                                                                |
|    noerr     | スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>コメント

-   このコマンドは、ベーシックディスクとダイナミックディスクで機能します。
-   このコマンドを成功させるには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

フォーカスがある MBR ディスクの署名を表示するには、次のように入力します。
```
uniqueid disk
```
5f1b2c36 にフォーカスがある MBR ディスクの署名を設定するには、次のように入力します。
```
uniqueid disk id=5f1b2c36
```
Baf784e7-6bbd-4cfb-aaac-e86c96e166ee にフォーカスがある GPT ディスクの識別子を設定するには、次のように入力します。
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

#### <a name="additional-references"></a>その他の参照情報

