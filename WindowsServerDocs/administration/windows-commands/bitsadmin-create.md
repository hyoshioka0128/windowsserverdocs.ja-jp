---
title: bitsadmin create
description: '**Bitsadmin create**の Windows コマンドトピックでは、指定された表示名を持つ転送ジョブを作成します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a922d9f15aff0a9bd064a7e987920adf3a9107d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850815"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された表示名を使用して転送ジョブを作成します。 ダウンロードジョブは、サーバーからローカルファイルにデータを転送します。 アップロードジョブは、ローカルファイルからサーバーにデータを転送します。 アップロード/応答ジョブは、ローカルファイルからサーバーにデータを転送し、サーバーから応答ファイルを受信します。

[Bitsadmin resume](bitsadmin-resume.md)スイッチを使用して、転送キュー内のジョブをアクティブ化します。

## <a name="syntax"></a>構文

```
bitsadmin /create [type] displayname
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| 型 | -  **/ダウンロード**は、サーバーからローカルファイルにデータを転送します。<p>-  **/アップロード**は、データをローカルファイルからサーバーに転送します。<p>-  **/uploadreply**は、ローカルファイルからサーバーにデータを転送し、サーバーから応答ファイルを受信します。<p>このパラメーターの既定値は、コマンドラインで指定されていない場合の**ダウンロード**です。 また、 **/Upload** および/ **upload ** の種類は、BITS 1.2 以前では使用できません。 |
| displayname | 新しく作成されたジョブに割り当てられた表示名。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

*Mydownloadjob*という名前のダウンロードジョブを作成します。

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
