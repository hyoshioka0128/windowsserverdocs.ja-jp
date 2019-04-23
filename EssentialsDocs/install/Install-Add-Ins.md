---
title: アドインのインストール
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62e4f07-c2ba-4c5e-b30c-bdc287cd654e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d00cb6886e812ee2b780ad79e1fba44442e279ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833073"
---
# <a name="install-add-ins"></a>アドインのインストール

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

イメージを作成する前にアドインをインストールすることで、すべてのサーバーまたはクライアント コンピューターにアドインを含めることができます。 これらのアドインは、そのイメージを使用してレプリケートされたすべてのコンピューターに自動的に含まれます。 1 個のアドインをインストールするには .wssx ファイルを実行します。または、アドインの種類ごとに [SDK ドキュメント](https://go.microsoft.com/fwlink/?LinkID=248648)のガイダンスに従って、個別のアドイン ファイルをインストールします。 .wssx ファイルを使用してインストールすると、アドイン マネージャーを通じてアドインをアンインストールできます。 個別のファイルをインストールする場合、アドインはアドイン マネージャーから管理されません。  
  
> [!NOTE]
>  サーバーにインストールまたはダウンロードされたソフトウェア (ダッシュボードのタブや正常性通知など) のインターフェイスは、サーバーにインストールされているオペレーティング システムと同じ言語にローカライズされている必要があります。  
  
#### <a name="to-install-an-add-in"></a>アドインをインストールするには  
  
1.  (省略可能) .wssx ファイルを使用してアドインをインストールしている場合、次の手順を完了します。  
  
    1.  保存、< アドイン名\>.wssx ファイル参照コンピューターにします。  
  
    2.  .wssx ファイルをダブルクリックして、アドインのインストール ウィザードを開きます。  
  
    3.  ウィザードの指示に従って、インストールを完了させます。  
  
2.  (省略可能) 個別のアドイン ファイルを、アドインの種類ごとに SDK で定義されたように適切な場所にインストールします。  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)