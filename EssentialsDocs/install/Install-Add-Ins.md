---
title: "Add-Ins をインストールします。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-add-ins"></a>Add-Ins をインストールします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

イメージを作成する前にそれらをインストールすることによって、すべてのサーバーまたはクライアント コンピューターにアドインを含めることができます。 これらのアドインはそのイメージを使用してレプリケートされたすべてのコンピューターに自動的に含まします。 .Wssx ファイルを実行してアドインをインストールできますか、または」のガイダンスに従って個別のアドイン ファイルをインストールすることができます、[SDK ドキュメント](https://go.microsoft.com/fwlink/?LinkID=248648)アドインの種類ごとにします。 .Wssx ファイルを使用してインストールする場合、アドインをアンインストールできます Add-In マネージャーを通じて。 個々 のファイルをインストールする場合、追加の管理されていない Add-In マネージャーから。  
  
> [!NOTE]
>  あるソフトウェアがインストールされているか (ダッシュ ボードのタブや正常性通知など)、サーバーにダウンロードするには、ローカライズされたインターフェイス、サーバーにインストールされているオペレーティング システムの言語に一致する必要があります。  
  
#### <a name="to-install-an-add-in"></a>アドインをインストールするには  
  
1.  (省略可能).Wssx ファイルを使用してアドインをインストールする場合は、次の手順を実行します。  
  
    1.  参照コンピューターで、< AddinName\ > .wssx ファイルを保存します。  
  
    2.  Add-in インストール ウィザードを開く .wssx ファイルをダブルクリックします。  
  
    3.  インストールの完了には、ウィザードの指示に従います。  
  
2.  (省略可能)アドインの種類ごとに SDK で定義されている適切な場所に個別のアドイン ファイルをインストールします。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)