---
title: bitsadmin addfilewithranges
description: Windows コマンド」のトピック**bitsadmin addfilewithranges** -指定されたジョブにファイルを追加します。 BITS では、リモート ファイルから指定した範囲をダウンロードします。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 081e5caeb7fb458b367f035b9995929de84a5528
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266569"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

指定したジョブには、ファイルを追加します。 BITS では、リモート ファイルから指定した範囲をダウンロードします。 このスイッチは、ダウンロード ジョブでのみ有効です。

## <a name="syntax"></a>構文

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|RemoteURL|*RemoteURL*は、サーバー上のファイルの URL です。|
|LocalName|*LocalName*ローカル コンピューター上のファイルの名前を指定します。 *LocalName*ファイルへの絶対パスを含める必要があります。|
|RangeList|*RangeList*がオフセットの長さ: ペアのコンマ区切りの一覧。 コロンを使用して、長さの値からオフセット値を区切ります。 たとえばの値`0:100,2000:100,5000:eof`からのオフセット 0、100 バイト オフセット 2000 から 100 バイトが転送には BITS を指示しから残りのバイト オフセット、ファイルの末尾に 5000 です。|

## <a name="more-information"></a>詳細情報

-   トークン**eof**オフセットと長さのペア内で有効な長さの値は、  *\<RangeList >* します。 サービスを指定したファイルの末尾まで読み取るように指示します。
-   長さ 0 の範囲を指定すると共に、同じオフセットは、別の範囲など AddFileWithRanges が失敗しエラー コード 0x8020002c ことに注意してください。C:\bits > bitsadmin/addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0、100:5

    エラー メッセージ:ジョブ - 0x8020002c にファイルを追加できません。 バイト範囲の一覧には、サポートされていない、重複する範囲が含まれています。

    回避策: は、長さ 0 の範囲を最初は指定できません。 例: bitsadmin/addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5、100:0 します。

## <a name="examples"></a>例

次の例からのオフセット 0、100 バイト オフセットの 2000 から 100 バイトが転送には BITS およびから残りのバイト オフセット 5000 ファイルの末尾にします。
```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip "0:100,2000:100,5000:eof"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)