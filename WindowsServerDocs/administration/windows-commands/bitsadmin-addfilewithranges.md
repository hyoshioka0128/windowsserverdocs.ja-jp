---
title: bitsadmin addfilewithranges
description: '**Bitsadmin addfilewithranges**の Windows コマンドに関するトピックでは、指定されたジョブにファイルを追加します。 BITS は、指定された範囲をリモートファイルからダウンロードします。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 557f19f6e106e5fb73b3a229090eecf0fc048758
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382021"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

指定されたジョブにファイルを追加します。 BITS は、指定された範囲をリモートファイルからダウンロードします。 このスイッチは、ダウンロードジョブに対してのみ有効です。

## <a name="syntax"></a>構文

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|RemoteURL|*Remoteurl*は、サーバー上のファイルの url です。|
|LocalName|*LocalName*ローカルコンピューター上のファイルの名前を指定します。 *LocalName*には、ファイルへの絶対パスが含まれている必要があります。|
|RangeList|*Rangelist*は、オフセットの長さをコンマで区切ったリストです。 長さの値からオフセット値を区切るには、コロンを使用します。 たとえば、値 `0:100,2000:100,5000:eof` の場合、オフセット0から100バイト、オフセット2000からの100バイト、およびオフセット5000からファイルの末尾までの残りのバイトを転送するビットを示します。|

## <a name="more-information"></a>詳細情報

-   トークン**eof**は、 *\<rangelist >* のオフセットと長さのペア内の有効な長さの値です。 このメソッドは、指定されたファイルの末尾に読み取るようにサービスに指示します。
-   0の長さの範囲が指定されていて、同じオフセットを持つ別の範囲が指定されている場合、AddFileWithRanges はエラーコード0x8020002c で失敗します。次に例を示します。C:\ ビット > bitsadmin/addfilewithranges j2 http://bitsdc/dload/1k.zip c:\ 1 k.zip 100: 0100: 5

    エラー メッセージ:ジョブにファイルを追加できません-0x8020002c。 バイト範囲の一覧に、重複する範囲が含まれていますが、これはサポートされていません。

    回避策: 最初に長さ0の範囲を指定しないでください。 例: bitsadmin/addfilewithranges j2 http://bitsdc/dload/1k.zip c:\-: 5100: 0

## <a name="examples"></a>使用例

次の例では、オフセット0から100バイト、オフセット2000からの100バイト、およびオフセット5000からファイルの末尾までの残りのバイトを転送するようにビットに指示します。

```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip "0:100,2000:100,5000:eof"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)