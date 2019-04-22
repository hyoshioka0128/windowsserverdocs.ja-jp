---
title: bitsadmin create
description: Windows コマンド」のトピック**bitsadmin 作成**-特定の表示名の転送ジョブを作成します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d6ce5a4fdc21d879bf0a265e3c4185d83311464a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817193"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した表示名の転送ジョブを作成します。 サーバーからローカル ファイルにジョブのデータ転送をダウンロードします。 ローカル ファイルからサーバーにデータを転送ジョブをアップロードします。 アップロード応答ジョブをサーバーにローカル ファイルからデータを転送し、サーバーから返信ファイルを受信します。

使用して、 [bitsadmin 再開](bitsadmin-resume.md)転送キュー内のジョブをアクティブにするスイッチ。

## <a name="syntax"></a>構文

```
bitsadmin /create [type] DisplayName
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|type|-   **/ダウンロード**サーバーからローカル ファイルにデータを転送します。<br />-   **/アップロード**サーバーにローカル ファイルからデータを転送します。<br />-   **/アップロード応答**サーバーにローカル ファイルからデータを転送し、サーバーから返信ファイルを受け取ります。<br />-このパラメーターの既定値**ダウンロード/** コマンドラインで指定されていない場合。|
|DisplayName|新しく作成されたジョブに割り当てられた表示名。|

**1.2 およびそれ以前の BITS**: /Upload と/Upload-Reply 型は使用できません。

## <a name="BKMK_examples"></a>例

という名前のダウンロード ジョブを作成します。 *myDownloadJob*します。

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>その他の参照

[コマンドライン構文キー](command-line-syntax-key.md)
