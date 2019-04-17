---
title: "インストールまたは言語パックを削除します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-or-remove-language-packs"></a>インストールまたは言語パックを削除します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

> [!NOTE]
>  多言語 Windows イメージを作成する必要があります最初、[言語パックと展開](https://technet.microsoft.com/library/hh824829)、Windows Server Essentials 言語パックを追加する前にします。  
  
 言語パックでは、多言語イメージの作成に使用できるのみです。 このセクションの情報は、インストールまたは Windows Server Essentials での言語パックの削除に固有です。  
  
> [!NOTE]
>  Ja-jp などの東アジア言語をサポートしていないクライアント コンピューターから初期構成 (IC) を実行して、サーバー上の多言語イメージに英語が含まれていない場合、IC の Web ページには四角形が表示されます。 既定を英語に IC の Web ページ、多言語イメージを作成するには、英語を含める必要があります。  
  
## <a name="adding-language-packs-to-an-image"></a>言語パックの追加をイメージに  
 言語パックは、OEM カスタマイズ DVD でご確認いただけます。 イメージに言語パックを追加する前に、テクニシャン コンピューターを言語パックをコピーすることをお勧めします。  
  
 次のコマンドを使用して、言語パックをインストールする必要があります。  
  
 **Dism.exe/online /Add-Package /PackagePath: C:\\ < cab ファイル directory\ への完全パス > \lp.cab**  
  
 たとえば、次のコマンドは、ドイツ語の言語パックを追加する方法を示しています。  
  
 **Dism.exe/online /Add-Package /PackagePath: C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
> [!IMPORTANT]
>  オペレーティング システムを完全にローカライズする Windows Server Essentials の言語パックも適用する必要があります。  
  
## <a name="removing-language-packs-from-an-image"></a>イメージから言語パックを削除します。  
 次のコマンドを使用すると、イメージに含める必要がなくなった言語パックを削除します。  
  
 **Dism.exe/online /Remove-Package /PackagePath: C:\\ < cab ファイル directory\ への完全パス > \lp.cab**  
  
 たとえば、次のコマンドは、ドイツ語の言語パックを削除する方法を示しています。  
  
 **Dism.exe/online /Remove-Package /PackagePath: C:\Users\Administrator\Desktop\WindowsHomeServer-Product-r\de-de\lp.cab**  
  
## <a name="see-also"></a>参照してください。  

 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

