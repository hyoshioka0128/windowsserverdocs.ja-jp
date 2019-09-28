---
title: bitsadmin setaclflag
description: '**Bitsadmin setaclflag**の Windows コマンドのトピック-アクセス制御リストの伝達フラグを設定します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fbdb12c29af7b4db8b25846d43ee1c93b2454ff2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380757"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

ジョブのアクセス制御リスト (ACL) の伝達フラグを設定します。 フラグは、ファイルをダウンロードするときに所有者と ACL の情報を保持することを示します。 たとえば、ファイルで所有者とグループを管理するには、 **フラグ**を  to `OG` に設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|フラグ|次のフラグの値を1つ以上指定します。</br>I/O所有者情報をファイルと共にコピーします。</br>A-G-DL-Pグループ情報をファイルと共にコピーします。</br>ADACL 情報をファイルと共にコピーします。</br>-S: ファイルを使用して SACL 情報をコピーします。|

## <a name="remarks"></a>コメント

SetAclFlags スイッチは、ジョブが Windows (SMB) 共有からデータをダウンロードするときに、所有者およびアクセス制御リストの情報を保持するために使用されます。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアクセス制御リストの伝達フラグを設定して、ダウンロードされたファイルで所有者とグループの情報を管理します。
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)