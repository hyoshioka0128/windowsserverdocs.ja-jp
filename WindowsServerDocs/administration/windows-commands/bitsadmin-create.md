---
title: bitsadmin create
description: '**Bitsadmin create**の Windows コマンドトピックでは、指定された表示名を持つ転送ジョブを作成します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f6d641d44c56ea4ff11f48a725367de7dcf472a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381808"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された表示名を使用して転送ジョブを作成します。 ダウンロードジョブは、サーバーからローカルファイルにデータを転送します。 アップロードジョブは、ローカルファイルからサーバーにデータを転送します。 アップロード/応答ジョブは、ローカルファイルからサーバーにデータを転送し、サーバーから応答ファイルを受信します。

[Bitsadmin resume](bitsadmin-resume.md)スイッチを使用して、転送キュー内のジョブをアクティブ化します。

## <a name="syntax"></a>構文

```
bitsadmin /create [type] DisplayName
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|type|-    **/ダウンロード**は、サーバーからローカルファイルにデータを転送します。<br />-    **/アップロード**は、データをローカルファイルからサーバーに転送します。<br />-    **/uploadreply**は、ローカルファイルからサーバーにデータを転送し、サーバーから応答ファイルを受信します。<br />-このパラメーターの既定値は、コマンドラインで指定されていない場合の**ダウンロード**です。|
|DisplayName|新しく作成されたジョブに割り当てられた表示名。|

**BITS 1.2 以前**: /Upload および/upload応答の種類は使用できません。

## <a name="BKMK_examples"></a>例

*Mydownloadjob*という名前のダウンロードジョブを作成します。

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
