---
title: "正常性アラートを追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 270e0aac-dc42-46f3-a20b-a68ffbded06d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cf0c062b92c687f5f7b33b419eafdca2dd3bbbfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-health-alerts"></a>正常性アラートを追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

正常性アドインは、アラート、正常性チェック、およびネットワークの問題の修復の定義を提供します。 正常性アドインはコードまたは特定の機能の正常性情報を評価するために使用されるデータをコメントする xml ファイルで構成されます。 正常性アドインは開発者によって作成され、管理者がサーバーとクライアント コンピューターにインストールされています。  
  
 参照してください、[Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)正常性アドインを作成する方法についてです。  
  
## <a name="installing-health-add-in-files"></a>正常性アドインのファイルをインストールします。  
 開発者が xml ファイルを作成した後、サーバーとクライアント コンピューターに適切な場所にファイルのコピーを配置する必要があります。  
  
#### <a name="to-install-the-xml-files-on-the-server"></a>サーバー上の xml ファイルをインストールするには  
  
1.  **%ProgramFiles%\Windows server \bin\feature Definitions**フォルダー、という名前の新しいフォルダーを作成する**MyHealthAddIn**します。 このフォルダーには、任意の名前を付けることができます。 フォルダーの名前が、機能の名前と同じであることをお勧めします。  
  
2.  Definition.xml ファイルと Definition.xml .config ファイルを新しいフォルダーにコピーします。  
  
3.  条件または操作のバイナリ ファイルを作成した場合は、それらのファイルをもコピーする必要があります**%ProgramFiles%\Windows server \bin**します。  
  
 クライアント コンピューターでは、適切な場所に XML ファイルをプルするスケジュールされたタスク 6 時間おきを実行します。 手動でタスクを実行して、クライアント コンピューターとサーバー間の同期を強制できます。  
  
#### <a name="to-install-the-xml-files-on-the-client-computer"></a>クライアント コンピューター上の xml ファイルをインストールするには  
  
1.  タスク スケジューラを開きます。  
  
2.  実行、**HealthDefintionUpdateTask**タスク スケジューラでします。  
  
    > [!NOTE]
    >  このタスクでは、バイナリ ファイルはインストールされません。 バイナリ ファイルを手動でコピーする必要があります、**%ProgramFiles%\Windows server \bin**クライアント コンピューター上のフォルダーです。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)