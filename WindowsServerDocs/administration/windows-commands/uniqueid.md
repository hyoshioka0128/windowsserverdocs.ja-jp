---
title: 一意の id
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4cad6607e13d2657433e4e78ce8e65beff73aa9d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857513"
---
# <a name="uniqueid"></a>一意の id



表示または GUID パーティション テーブル (GPT) の識別子またはマスター ブート レコード (MBR) の署名、フォーカスがあるディスクを設定します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のエディションでご利用いただけません。

## <a name="syntax"></a>構文

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|id={\<dword> | <GUID>}|MBR ディスクでは、署名の 16 進数形式で 4 バイト (DWORD) 値を指定します。</br>GPT ディスクの場合は、識別子の GUID を指定します。|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   このコマンドは、ベーシック ディスクとダイナミック ディスクで機能します。
-   このコマンドを成功させるには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

MBR ディスクでは、フォーカスのシグネチャを表示するには、次のように入力します。
```
uniqueid disk
```
MBR ディスクでは、フォーカスのシグネチャを 5f1b2c36 を設定するには、次のように入力します。
```
uniqueid disk id=5f1b2c36
```
Baf784e7-6bbd-4cfb-aaac-e86c96e166ee にフォーカスを持つ GPT ディスクの識別子を設定するには、次のように入力します。
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

#### <a name="additional-references"></a>その他の参照情報

