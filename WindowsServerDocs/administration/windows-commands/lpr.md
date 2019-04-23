---
title: lpr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afc8790b-8b52-45c4-acdf-be0ffa9da534 jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e21b1606b09c47ea773c4fad80eaa53d9aca27c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888753"
---
# <a name="lpr"></a>lpr

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コンピューターまたはプリンターの印刷の準備として、ライン プリンタ デーモン (LPD) サービスを実行しているデバイスを共有するには、ファイルを送信します。  
  
## <a name="syntax"></a>構文  
```  
lpr [-S <ServerName>] -P <printerName> [-C <BannerContent>] [-J <JobName>] [-o | "-o l"] [-x] [-d] <filename>  
```  
## <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|-S <ServerName>|コンピューターまたはプリンターの共有状態を表示したい LPD 印刷キューをホストしているデバイス (名前または IP アドレス) を指定します。 必須。|  
|-P <printerName>|表示する状態で印刷キューのプリンターを (名) を指定します。 必須。|  
|C <BannerContent>|印刷ジョブのバナーのページに印刷する内容を指定します。 このパラメーターを含めない場合、印刷ジョブの送信元コンピューターの名前は [バナー] ページが表示されます。|  
|-J <JobName>|[バナー] ページで印刷される印刷ジョブの名前を指定します。 このパラメーターを指定しないと、バナーのページに印刷されているファイルの名前が表示されます。|  
|[、o&#124; "-l o"]|印刷するファイルの種類を指定します。 パラメーター **-o**テキスト ファイルを印刷することを指定します。 パラメーター **"-l o"** バイナリ ファイル (たとえば、PostScript ファイル) を印刷することを指定します。|  
|-d|コントロール ファイルの前に、データ ファイルを送信する必要がありますを指定します。 プリンターが最初に送信されるデータ ファイルが必要な場合は、このパラメーターを使用します。 詳細については、プリンターのマニュアルを参照してください。|  
|-x|指定します、 **lpr**コマンドは、オペレーティング システム (SunOS と呼ばれます) のリリースまでなど、4.1.4_u1 Sun Microsystems との互換性である必要があります。|  
|<FileName>|印刷するファイル (その名前) を指定します。 必須。|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="remarks"></a>注釈  
-   プリンターの名前を検索するには、[プリンタ] フォルダを開きます。  
-   **-S**、 **-p**、 **-c**、および **-j**パラメーターは大文字と小文字、大文字で入力する必要があります。  
## <a name="BKMK_examples"></a>例  
この例では、LPD 10.0.0.45 にホスト上の Laserprinter1 プリンター キューに"Document.txt"テキスト ファイルを印刷する方法を示します。  
```  
lpr -S 10.0.0.45 -P Laserprinter1 -o Document.txt  
```  
この例では、10.0.0.45 で LPD ホスト上の Laserprinter1 プリンター キューに"PostScript_file.ps"PostScript ファイルを印刷する方法を示します。  
```  
lpr -S 10.0.0.45 -P Laserprinter1 "-o l" PostScript_file.ps  
```  

#### <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
-   [印刷コマンドのリファレンス](print-command-reference.md)  
