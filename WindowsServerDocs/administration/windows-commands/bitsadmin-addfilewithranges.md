---
title: bitsadmin addfilewithranges
description: '**Bitsadmin addfilewithranges**の Windows コマンドに関するトピックでは、指定されたジョブにファイルを追加します。 BITS は、指定された範囲をリモートファイルからダウンロードします。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60b448550473691bbbaf573f99f00609e14e0f42
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850955"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

指定されたジョブにファイルを追加します。 BITS は、指定された範囲をリモートファイルからダウンロードします。 このスイッチは、ダウンロードジョブに対してのみ有効です。

## <a name="syntax"></a>構文

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| Job | ジョブの表示名または GUID。 |
| RemoteURL | サーバー上のファイルの URL。 |
| LocalName | ローカルコンピューター上のファイルの名前。 ファイルへの絶対パスが含まれている必要があります。 |
| RangeList | オフセットの長さのコンマ区切りの一覧。 長さの値からオフセット値を区切るには、コロンを使用します。 たとえば、`0:100,2000:100,5000:eof` の値は、オフセット0から100バイト、オフセット2000からの100バイト、およびオフセット5000からファイルの末尾までの残りのバイトを転送するようにビットに指示します。 |

## <a name="remarks"></a>コメント

- トークン**eof**は、 *\<rangelist >* のオフセットと長さのペア内の有効な長さの値です。 このメソッドは、指定されたファイルの末尾に読み取るようにサービスに指示します。

- 次のように、ゼロ長の範囲が同じオフセットを持つ別の範囲と共に指定されている場合、AddFileWithRanges はエラーコード0x8020002c で失敗します。

    `C:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **エラーメッセージ:** ジョブにファイルを追加できません-0x8020002c。 バイト範囲の一覧に、重複する範囲が含まれていますが、これはサポートされていません。

    **回避策:** 最初に長さ0の範囲を指定しないでください。 たとえば、次のように指定します。 

    `bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0.`

## <a name="examples"></a>例

次の例では、オフセット0から100バイト、オフセット2000からの100バイト、およびオフセット5000からファイルの末尾までの残りのバイトを転送するようにビットに指示します。

```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)