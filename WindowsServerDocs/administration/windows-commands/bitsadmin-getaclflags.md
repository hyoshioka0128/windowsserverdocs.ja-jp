---
title: bitsadmin getaclflags
description: Windows コマンド」のトピック**bitsadmin getaclflags** -アクセス制御リストの反映フラグを取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 185445a97168344f910abc0e644718296de2c712
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861453"
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

## <a name="remarks"></a>注釈

次のフラグの値の 1 つ以上が表示されます。
-   O:ファイルの所有者情報をコピーします。
-   G:ファイル グループ情報をコピーします。
-   D:DACL 情報をファイルにコピーします。
-   送信:ファイルの SACL の情報をコピーします。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブへのアクセス制御リスト伝達フラグを取得する*myDownloadJob*します。
```
C:\>bitsadmin /getaclflags myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)