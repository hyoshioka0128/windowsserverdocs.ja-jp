---
title: 言語パックのインストールまたは削除
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c1fd1d21277d32672398d1dd201e2dda24682c2d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820025"
---
# <a name="install-or-remove-language-packs"></a>言語パックのインストールまたは削除

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

> [!NOTE]
>  まず、「[言語パックと展開](https://technet.microsoft.com/library/hh824829)」で説明されているように、Windows Server Essentials 言語パックを追加する前に、多言語の Windows イメージを作成する必要があります。  
  
 言語パックは、多言語イメージを作成する場合にのみ使用できます。 このセクションの情報は、Windows Server Essentials での言語パックのインストールまたは削除に固有のものです。  
  
> [!NOTE]
>  ja-jp などの東アジア言語をサポートしていないクライアント コンピューターから初期構成 (IC) を実行する場合、およびサーバーの多言語イメージに英語が含まれていない場合、IC の Web ページの文字が四角形として表示されます。 IC の Web ページの既定を英語にするには、作成する多言語イメージに英語を含める必要があります。  
  
## <a name="adding-language-packs-to-an-image"></a>イメージへの言語パックの追加  
 言語パックは、OEM カスタマイズ DVD に含まれています。 イメージに言語パックを追加する前に、言語パックをテクニシャン コンピューターにコピーすることをお勧めします。  
  
 言語パックをインストールするには、次のコマンドを使用する必要があります。  
  
 **dism.exe/online/Add-Package/PackagePath: C:\\< cab ファイルディレクトリへの完全パス\>**  
  
 たとえば、次のコマンドはドイツ語の言語パックを追加する方法を示します。  
  
 **dism.exe/online/Add-Package/PackagePath: C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  また、オペレーティングシステムを完全にローカライズするには、Windows Server Essentials の言語パックも適用する必要があります。  
  
## <a name="removing-language-packs-from-an-image"></a>イメージからの言語パックの削除  
 イメージに含める必要がなくなった言語パックを削除するには、次のコマンドを使用します。  
  
 **dism.exe/online/Remove-Package/PackagePath: C:\\< cab ファイルディレクトリへの完全パス\>**  
  
 たとえば、次のコマンドはドイツ語の言語パックを削除する方法を示します。  
  
 **dism.exe/online/Remove-Package/PackagePath: C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>参照  

 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [イメージ  の作成とカスタマイズ](../install/Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [展開  のイメージの準備](../install/Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

