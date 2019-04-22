---
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
title: fsutil の objectid
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 2f5887f20e2c36ec7dcfcd6f4e920b5273c6c60c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813743"
---
# <a name="fsutil-objectid"></a>fsutil の objectid
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7

ファイル、ディレクトリ、およびリンクなどの他のオブジェクトを追跡するために、分散リンクの追跡 (DLT) クライアントのサービスおよびファイル レプリケーション サービス (FRS) によって使用される内部のオブジェクトはオブジェクト識別子 (Oid) を管理します。 オブジェクト識別子は、ほとんどのプログラムに表示されないし、変更しないでください。

> [!CAUTION]
> 削除、設定、またはしないでそれ以外の場合、オブジェクト識別子を変更します。 削除するか、オブジェクト識別子の設定は、すべてのデータ ボリュームを含む、ファイルの部分からのデータが失われる可能性します。 さらに、分散リンクの追跡 (DLT) クライアントのサービスとファイル レプリケーション サービス (FRS) で有害な動作が発生する可能性があります。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil objectid [create] <FileName>
fsutil objectid [delete] <FileName>
fsutil objectid [query] <FileName>
fsutil objectid [set] <ObjectID> <BirthVolumeID> <BirthObjectID> <DomainID> <FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|作成|指定したファイルがまだない場合 1 つは、オブジェクト識別子を作成します。 ファイルは、オブジェクト識別子を既に持っている場合、このサブコマンドは同じです、**クエリ**サブコマンドします。|
|delete|オブジェクト識別子を削除します。|
|クエリ (query)|オブジェクト識別子を照会します。|
|セット (set)|オブジェクト識別子を設定します。|
|\<ObjectID>|ボリューム内で一意であることが保証される特定のファイルの 16 バイトの 16 進識別子を設定します。 オブジェクト識別子は、ファイルを識別するために、分散リンクの追跡 (DLT) クライアント サービスとファイル レプリケーション サービス (FRS) によって使用されます。|
|\<BirthVolumeID>|ファイルが配置されている場合、最初に、オブジェクト識別子を取得してボリュームを示します。 この値は、DLT クライアント サービスで使用される 16 バイトの 16 進識別子です。|
|\<BirthObjectID>|ファイルの元のオブジェクト識別子を示します (、 *ObjectID*ファイルが移動されると変わる可能性があります)。 この値は、DLT クライアント サービスで使用される 16 バイトの 16 進識別子です。|
|\<DomainID >|16 バイトの 16 進数のドメイン識別子です。 この値は、現在使用されていないと、すべてゼロに設定する必要があります。|
|\<FileName>|ファイル名と拡張子、たとえば C:\documents\filename.txt を含むファイルへの完全パスを指定します。|

## <a name="remarks"></a>注釈

-   オブジェクト識別子を持つ任意のファイルは、生年月日ボリュームの識別子、生年月日のオブジェクト識別子、およびドメイン識別子もあります。 ファイルを移動するときは、オブジェクト識別子を変更することがありますが、生年月日のボリュームと生年月日のオブジェクト識別子は変化します。 この動作により、常に移動された場所に関係なく、ファイルを検索する Windows オペレーティング システムです。

## <a name="BKMK_examples"></a>例
オブジェクト識別子を作成するには、次のように入力します。

`fsutil objectid create c:\temp\sample.txt`

オブジェクト識別子を削除するには、次のように入力します。

`fsutil objectid delete c:\temp\sample.txt`

オブジェクト識別子をクエリするには、次のように入力します。

`fsutil objectid query c:\temp\sample.txt`

オブジェクト識別子を設定するには、次のように入力します。

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


