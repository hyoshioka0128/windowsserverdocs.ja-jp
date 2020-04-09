---
title: bitsadmin getaclflags
description: '**Bitsadmin getaclflags**の Windows コマンドに関するトピックでは、アクセス制御リスト (ACL) の伝達フラグを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d53018e2fa5c659c8cf4b0ec985beda848a8c1af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850795"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

項目が子オブジェクトによって継承されているかどうかを示すアクセス制御リスト (ACL) の伝達フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getaclflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="remarks"></a>コメント

次のフラグ値の1つまたは複数を表示します。

- **o** -所有者の情報をファイルにコピーします。

- **g** -グループ情報をファイルと共にコピーします。

- **d** -随意アクセス制御リスト (DACL) の情報をファイルと共にコピーします。

- **s** -システムアクセス制御リスト (SACL) の情報をファイルにコピーします。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアクセス制御リストの伝達フラグを取得します。

```
C:\>bitsadmin /getaclflags myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)