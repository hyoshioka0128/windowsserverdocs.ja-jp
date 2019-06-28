---
title: rdpsign
description: RDP ファイルにデジタル署名する方法をについて説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a6fa8ce-3d32-49a5-b056-bcc1a23391f5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 9e35d3a3e85ed046fb658bbf5a97ab5fc5eec6d3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442012"
---
# <a name="rdpsign"></a>rdpsign

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ プロトコル (.rdp) ファイルにデジタル署名することできます。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|/sha1 \<hash>|これは、セキュア ハッシュ アルゴリズム 1 (SHA1) ハッシュ、証明書ストアに含まれている署名証明書の拇印を指定します。|
|/q|Quiet モードです。 コマンドが成功すると、出力なしは、コマンドが失敗した場合は、最小限の出力。|
|/v|詳細モード。 すべての警告、メッセージ、および状態を表示します。|
|/l|実際には、入力ファイルのいずれかを置き換えることがなく、署名と出力の結果をテストします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   SHA1 証明書の拇印は、信頼済みの .rdp ファイルの発行元を表す必要があります。 証明書の拇印を取得する証明書スナップインを開く、] をクリックします (ローカル コンピューターの証明書ストアまたは個人証明書ストアに) を使用する証明書をダブルクリックして、**詳細**タブで、し、**フィールド**一覧で、[**拇印**します。

    > [!NOTE]
    > Rdpsign.exe ツールで使用するための拇印をコピーする場合は、スペースを削除する必要があります。

-   完全なファイル名を使用して署名する .rdp ファイル (複数可) を指定する必要があります。 ワイルドカード文字は使用できません。
-   符号付きの出力ファイルは、入力ファイルで上書きされます。
-   .rdp ファイルのいずれかは、読み取りまたは書き込みをすることはできない場合は、複数のファイルが指定されている場合に、ツールは次のファイルに引き続き。

## <a name="BKMK_examples"></a>例
- File1.rdp の名前は、.rdp ファイルをサインインするには、.rdp ファイルを保存したフォルダーに移動し、し、次のように入力します。
  ```
  rdpsign /sha1 hash file1.rdp
  ```
  > [!NOTE]
  > *ハッシュ* 値はスペースを含めないの SHA1 証明書の拇印を表します。
- .Rdp ファイルを実際には、ファイルへの署名せずにデジタル署名が成功したかどうかをテストするには、次のように入力します。
  ```
  rdpsign /sha1 hash /l file1.rdp
  ```
- 複数の .rdp ファイルを署名するには、スペースを使用して、ファイル名を区切ります。 たとえば、File1.rdp、File2.rdp、および File3.rdp という複数の .rdp ファイルをサインインするには、次のように入力します。
  ```
  rdpsign /sha1 hash file1.rdp file2.rdp file3.rdp
  ```
  ## <a name="see-also"></a>関連項目
  [コマンドライン構文キー](command-line-syntax-key.md)
  [リモート デスクトップ サービスと&#40;です。ターミナル サービスと&#41;です。コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
