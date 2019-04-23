---
title: bitsadmin setaclflag
description: Windows コマンド」のトピック**bitsadmin setaclflag** -アクセス制御リスト反映フラグを設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89d825a4bc4512022fed98a3188537d3977fa3c3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867403"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

ジョブのリスト (ACL) の反映フラグ、アクセス制御を設定します。 フラグでは、ダウンロードされるファイルの所有者と ACL の情報を維持することを指定します。 たとえば、ファイルの所有者とグループを維持するために次のように設定します。 **フラグ** に`OG`します。

## <a name="syntax"></a>構文

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|フラグ|次のフラグの値の 1 つ以上を指定します。</br>-/O:ファイルの所有者情報をコピーします。</br>-G:ファイル グループ情報をコピーします。</br>-D:DACL 情報をファイルにコピーします。</br>-S: コピー SACL 情報ファイルを使用します。|

## <a name="remarks"></a>注釈

SetAclFlags スイッチは、Windows (SMB) 共有からのデータのダウンロードには、ジョブの所有者とアクセス制御リストの情報の管理に使用されます。

## <a name="BKMK_examples"></a>例

次の例では、設定、アクセス制御リストという名前のジョブのフラグと反映フラグ*myDownloadJob*ダウンロードしたファイルを所有者とグループの情報を維持します。
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)