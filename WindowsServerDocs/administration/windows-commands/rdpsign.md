---
title: rdpsign
description: RDP ファイルにデジタル署名する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 406563a07d3760c2846c201410f3a7b8f1c2829b
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72588056"
---
# <a name="rdpsign"></a>rdpsign

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ プロトコル (.rdp) ファイルにデジタル署名することできます。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
rdpsign /sha1 <hash> [/q | /v |] [/l] <file_name.rdp>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|/sha1 \<hash >|これは、セキュア ハッシュ アルゴリズム 1 (SHA1) ハッシュ、証明書ストアに含まれている署名証明書の拇印を指定します。 Windows Server 2012 R2 以前で使用されています。|
|/sha256 \<hash >|証明書ストアに含まれる署名証明書のセキュアハッシュアルゴリズム 256 (SHA256) ハッシュであるサムプリントを指定します。 Windows Server 2016 以降の/sha1 を置き換えます。|
|/q|Quiet モードです。 コマンドが成功すると、出力なしは、コマンドが失敗した場合は、最小限の出力。|
|/v|詳細モード。 すべての警告、メッセージ、および状態を表示します。|
|/l|実際には、入力ファイルのいずれかを置き換えることがなく、署名と出力の結果をテストします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   SHA1 または SHA256 証明書の拇印は、信頼された .rdp ファイルの発行元を表す必要があります。 証明書の拇印を取得するには、証明書スナップインを開き、使用する証明書をダブルクリックします (ローカルコンピューターの証明書ストアまたは個人証明書ストアのいずれか)。 **詳細** タブ**をクリックし、フィールド**の一覧で **拇印** をクリックします。

    > [!NOTE]
    > Rdpsign ツールで使用するために拇印をコピーする場合は、スペースを削除する必要があります。

-   完全なファイル名を使用して署名する .rdp ファイル (複数可) を指定する必要があります。 ワイルドカード文字は使用できません。
-   符号付きの出力ファイルは、入力ファイルで上書きされます。
-   いずれかの .rdp ファイルの読み取りまたは書き込みができない場合、複数のファイルが指定されていると、ツールは次のファイルに進みます。

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
  ## <a name="see-also"></a>参照
  [コマンドライン構文キー](command-line-syntax-key.md)
  [リモート デスクトップ サービスと #40 です。ターミナル サービスと #41 です。コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
