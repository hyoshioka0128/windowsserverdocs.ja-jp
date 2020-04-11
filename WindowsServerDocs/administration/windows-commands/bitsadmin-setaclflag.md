---
title: bitsadmin setaclflag
description: '**Bitsadmin setaclflag**の Windows コマンドに関するトピックでは、アクセス制御リスト (ACL) の伝達フラグを設定しています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0aae550e94d04db518edccafb1d6bcf46d0320b
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123062"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

ジョブのアクセス制御リスト (ACL) の伝達フラグを設定します。 フラグは、ファイルをダウンロードするときに所有者と ACL の情報を保持することを示します。 たとえば、ファイルで所有者とグループを管理するには、 **flags**パラメーターを `og`に設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setaclflag <job> <flags>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| flags | 次のように、1つまたは複数の値を指定します。<ul><li>**o** -所有者の情報をファイルにコピーします。</li><li>**g** -グループ情報をファイルと共にコピーします。</li><li>**d** -随意アクセス制御リスト (DACL) の情報をファイルと共にコピーします。</li><li>**s** -システムアクセス制御リスト (SACL) の情報をファイルにコピーします。</li></ul> |

## <a name="remarks"></a>コメント

/Setaclflag スイッチは、ジョブが Windows (SMB) 共有からデータをダウンロードするときに、所有者とアクセス制御リストの情報を保持するために使用されます。

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアクセス制御リストの伝達フラグを設定して、ダウンロードされたファイルで所有者とグループの情報を管理します。

```
C:\>bitsadmin /setaclflags myDownloadJob og
```

## <a name="additional-references"></a>その他の参照情報

[コマンドライン構文のキー](command-line-syntax-key.md)&reg;'    