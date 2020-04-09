---
title: アドインのインストール
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: e62e4f07-c2ba-4c5e-b30c-bdc287cd654e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f8428a0198459e1dc036647a3d47fa1a49c00c01
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820135"
---
# <a name="install-add-ins"></a>アドインのインストール

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

イメージを作成する前にアドインをインストールすることで、すべてのサーバーまたはクライアント コンピューターにアドインを含めることができます。 これらのアドインは、そのイメージを使用してレプリケートされたすべてのコンピューターに自動的に含まれます。 1 個のアドインをインストールするには .wssx ファイルを実行します。または、アドインの種類ごとに [SDK ドキュメント](https://go.microsoft.com/fwlink/?LinkID=248648)のガイダンスに従って、個別のアドイン ファイルをインストールします。 .wssx ファイルを使用してインストールすると、アドイン マネージャーを通じてアドインをアンインストールできます。 個別のファイルをインストールする場合、アドインはアドイン マネージャーから管理されません。  
  
> [!NOTE]
>  サーバーにインストールまたはダウンロードされたソフトウェア (ダッシュボードのタブや正常性通知など) のインターフェイスは、サーバーにインストールされているオペレーティング システムと同じ言語にローカライズされている必要があります。  
  
#### <a name="to-install-an-add-in"></a>アドインをインストールするには  
  
1.  (省略可能) .wssx ファイルを使用してアドインをインストールしている場合、次の手順を完了します。  
  
    1.  < AddinName\>wssx ファイルを参照コンピューターに保存します。  
  
    2.  .wssx ファイルをダブルクリックして、アドインのインストール ウィザードを開きます。  
  
    3.  ウィザードの指示に従って、インストールを完了します。  
  
2.  (省略可能) 個別のアドイン ファイルを、アドインの種類ごとに SDK で定義されたように適切な場所にインストールします。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)