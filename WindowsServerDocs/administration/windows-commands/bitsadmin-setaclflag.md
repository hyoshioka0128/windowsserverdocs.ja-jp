---
title: bitsadmin setaclflag
description: Bitsadmin setaclflag の Windows コマンドに関するトピックでは、アクセス制御リストの伝達フラグを設定しています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4ac47e554dde6a555e891d89668cd12fec3179d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849675"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

ジョブのアクセス制御リスト (ACL) の伝達フラグを設定します。 フラグは、ファイルをダウンロードするときに所有者と ACL の情報を保持することを示します。 たとえば、ファイルで所有者とグループを管理するには、 **フラグ**を `OG`に設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetAclFlags <Job> <Flags>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|フラグ|次のフラグの値を1つ以上指定します。</br>-O: 所有者の情報をファイルにコピーします。</br>-G: グループ情報をファイルと共にコピーします。</br>-D: DACL 情報をファイルと共にコピーします。</br>-S: ファイルを使用して SACL 情報をコピーします。|

## <a name="remarks"></a>コメント

SetAclFlags スイッチは、ジョブが Windows (SMB) 共有からデータをダウンロードするときに、所有者およびアクセス制御リストの情報を保持するために使用されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアクセス制御リストの伝達フラグを設定して、ダウンロードされたファイルで所有者とグループの情報を管理します。
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)