---
title: bitsadmin addfilewithranges
description: Bitsadmin addfilewithranges コマンドの参照記事。指定されたジョブにファイルを追加します。 BITS は、指定された範囲をリモートファイルからダウンロードします。
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c19c6dfec23cf012f42ab7d10b1d3df90ca957ff
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894872"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

指定されたジョブにファイルを追加します。 BITS は、指定された範囲をリモートファイルからダウンロードします。 このスイッチは、ダウンロードジョブに対してのみ有効です。

## <a name="syntax"></a>構文

```
bitsadmin /addfilewithranges <job> <remoteURL> <localname> <rangelist>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| remoteURL | サーバー上のファイルの URL。 |
| localname | ローカルコンピューター上のファイルの名前。 ファイルへの絶対パスが含まれている必要があります。 |
| rangelist | オフセットの長さのコンマ区切りの一覧。 長さの値からオフセット値を区切るには、コロンを使用します。 たとえば、値がの場合は、オフセット `0:100,2000:100,5000:eof` 0 から100バイト、オフセット2000からの100バイト、およびオフセット5000からファイルの末尾までの残りのバイトを転送するようにビットに指示します。 |

## <a name="remarks"></a>Remarks

- トークン**eof**は、のオフセットと長さのペア内の有効な長さの値です `<rangelist>` 。 このメソッドは、指定されたファイルの末尾に読み取るようにサービスに指示します。

- `addfilewithranges`長さ0の範囲が同じオフセットを使用して別の範囲と共に指定されている場合、コマンドはエラーコード0x8020002c で失敗します。次に例を示します。

    `c:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **エラーメッセージ:** ジョブにファイルを追加できません-0x8020002c。 バイト範囲の一覧に、重複する範囲が含まれていますが、これはサポートされていません。

    **回避策:** 最初に長さ0の範囲を指定しないでください。 たとえば、`bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0` を使用します

## <a name="examples"></a>例

オフセット0から100バイト、オフセット2000から100バイトを転送し、残りのバイトをオフセット5000からファイルの末尾まで転送するには、次の手順を実行します。

```
bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
