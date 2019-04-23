---
title: 正常性アラートの追加
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828513"
---
# <a name="add-health-alerts"></a>正常性アラートの追加

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

正常性アドインは、アラートの定義、正常性チェック、ネットワークの問題の修復を提供します。 正常性アドインは、特定の機能の正常性情報を評価するために使用されるコードまたはデータをコメントする xml ファイルから構成されます。 正常性アドインは、開発者によって作成され、管理者によってサーバーとクライアント コンピューターにインストールされます。  
  
 正常性アドインの作成の詳細については、 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648) を参照してください。  
  
## <a name="installing-health-add-in-files"></a>正常性アドインのファイルをインストールする  
 開発者による xml ファイルの作成後、ファイルのコピーをサーバーとクライアント コンピューター上の適切な場所に配置する必要があります。  
  
#### <a name="to-install-the-xml-files-on-the-server"></a>XML ファイルをサーバーにインストールするには  
  
1.  **%ProgramFiles%\Windows Server\Bin\Feature Definitions** フォルダーで、 **MyHealthAddIn**という名前の新しいフォルダーを作成します。 このフォルダーには、任意の名前を付けることができます。 フォルダーの名前は、機能名と同じにすることを推奨します。  
  
2.  Definition.xml ファイルと Definition.xml.config ファイルを新しいフォルダーにコピーします。  
  
3.  条件または操作用にバイナリ ファイルを作成した場合、これらのファイルも **%ProgramFiles%\Windows Server\Bin**にコピーする必要があります。  
  
 クライアント コンピューターが、XML ファイルを適切な場所に抽出するスケジュールされたタスクを 6 時間ごとに実行します。 クライアント コンピューターとサーバーを強制的に同期させるには、このタスクを手動で実行します。  
  
#### <a name="to-install-the-xml-files-on-the-client-computer"></a>XML ファイルをクライアント コンピューターにインストールするには  
  
1.  タスク スケジューラを開きます。  
  
2.  タスク スケジューラで **HealthDefintionUpdateTask** を実行します。  
  
    > [!NOTE]
    >  このタスクでは、バイナリ ファイルはインストールされません。 バイナリ ファイルは、クライアント コンピューターの **%ProgramFiles%\Windows Server\Bin** フォルダーに手動でコピーする必要があります。  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)