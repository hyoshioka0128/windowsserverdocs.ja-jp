---
title: 言語パックのインストールまたは削除
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98f13f63-4480-40ba-a7ef-d1d9b7582e5f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a41b491bbe4b4a8ee7f9743dc85e5bdaffb08496
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860093"
---
# <a name="install-or-remove-language-packs"></a>言語パックのインストールまたは削除

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

> [!NOTE]
>  多言語 Windows イメージを作成する必要があります最初、[言語パックと展開](https://technet.microsoft.com/library/hh824829)Windows Server Essentials 言語パックを追加する前にします。  
  
 言語パックは、多言語イメージを作成する場合にのみ使用できます。 このセクションの情報は、インストールまたは Windows Server Essentials での言語パックを削除するのに固有です。  
  
> [!NOTE]
>  ja-jp などの東アジア言語をサポートしていないクライアント コンピューターから初期構成 (IC) を実行する場合、およびサーバーの多言語イメージに英語が含まれていない場合、IC の Web ページの文字が四角形として表示されます。 IC の Web ページの既定を英語にするには、作成する多言語イメージに英語を含める必要があります。  
  
## <a name="adding-language-packs-to-an-image"></a>イメージへの言語パックの追加  
 言語パックは、OEM カスタマイズ DVD に含まれています。 イメージに言語パックを追加する前に、言語パックをテクニシャン コンピューターにコピーすることをお勧めします。  
  
 言語パックをインストールするには、次のコマンドを使用する必要があります。  
  
 **dism.exe/online/Add-Package/PackagePath:C:\\< cab ファイルのディレクトリにフルパス\>\lp.cab**  
  
 たとえば、次のコマンドはドイツ語の言語パックを追加する方法を示します。  
  
 **dism.exe /online /Add-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  オペレーティング システムを完全にローカライズする Windows Server Essentials の言語パックを適用することも必要があります。  
  
## <a name="removing-language-packs-from-an-image"></a>イメージからの言語パックの削除  
 イメージに含める必要がなくなった言語パックを削除するには、次のコマンドを使用します。  
  
 **dism.exe /online /Remove-Package /PackagePath:C:\\<full path to cab file directory\>\lp.cab**  
  
 たとえば、次のコマンドはドイツ語の言語パックを削除する方法を示します。  
  
 **dism.exe /online /Remove-Package /PackagePath:C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>関連項目  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

