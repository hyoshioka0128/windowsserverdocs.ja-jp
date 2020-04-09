---
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
title: Fsutil objectid
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: e39b36a6c3126429bc47d5b89d104612cab5db96
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844285"
---
# <a name="fsutil-objectid"></a>Fsutil objectid
>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

オブジェクト識別子 (Oid) を管理します。 Oid は、分散リンク追跡 (DLT) クライアントサービスとファイルレプリケーションサービス (FRS) によって、ファイル、ディレクトリ、リンクなどの他のオブジェクトを追跡するために使用される内部オブジェクトです。 オブジェクト識別子はほとんどのプログラムでは見えないため、変更しないでください。

> [!CAUTION]
> オブジェクト識別子の削除、設定、または変更を行わないでください。 オブジェクト識別子を削除または設定すると、ファイルの一部のデータが失われる可能性があります。これは、データのボリューム全体に対して行われます。 また、分散リンク追跡 (DLT) クライアントサービスとファイルレプリケーションサービス (FRS) の動作が悪影響を及ぼす可能性があります。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil objectid [create] <FileName>
fsutil objectid [delete] <FileName>
fsutil objectid [query] <FileName>
fsutil objectid [set] <ObjectID> <BirthVolumeID> <BirthObjectID> <DomainID> <FileName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|作成|指定したファイルに存在しない場合は、オブジェクト識別子を作成します。 ファイルに既にオブジェクト識別子が含まれている場合、このサブコマンドは**query**サブコマンドと同じです。|
|削除|オブジェクト識別子を削除します。|
|query|オブジェクト識別子を照会します。|
|set|オブジェクト識別子を設定します。|
|\<ObjectID >|ボリューム内で一意であることが保証されるファイル固有の16バイトの16進数識別子を設定します。 オブジェクト識別子は、分散リンク追跡 (DLT) クライアントサービスとファイルレプリケーションサービス (FRS) がファイルを識別するために使用されます。|
|\<BirthVolumeID >|オブジェクト識別子を最初に取得したときにファイルが配置されたボリュームを示します。 この値は、DLT クライアントサービスによって使用される16バイトの16進数識別子です。|
|\<BirthObjectID >|ファイルの元のオブジェクト識別子を示します (ファイルの移動時に*ObjectID*が変更される可能性があります)。 この値は、DLT クライアントサービスによって使用される16バイトの16進数識別子です。|
|\<DomainID >|16バイトの16進数ドメイン識別子。 この値は現在使用されていないため、すべてゼロに設定する必要があります。|
|\<ファイル名 >|ファイル名と拡張子を含むファイルへの完全パスを指定します (例 C:\documents\filename.txt.)。|

## <a name="remarks"></a>コメント

-   オブジェクト識別子を持つすべてのファイルには、誕生日のボリューム識別子、生のオブジェクト識別子、およびドメイン識別子も含まれています。 ファイルを移動すると、オブジェクト識別子が変更される場合がありますが、誕生日のボリュームと生のオブジェクトの識別子は変わりません。 この動作により、Windows オペレーティングシステムは、移動された場所に関係なく、常にファイルを見つけることができます。

## <a name="examples"></a><a name="BKMK_examples"></a>例
オブジェクト識別子を作成するには、次のように入力します。

`fsutil objectid create c:\temp\sample.txt`

オブジェクト識別子を削除するには、次のように入力します。

`fsutil objectid delete c:\temp\sample.txt`

オブジェクト識別子を照会するには、次のように入力します。

`fsutil objectid query c:\temp\sample.txt`

オブジェクト識別子を設定するには、次のように入力します。

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


