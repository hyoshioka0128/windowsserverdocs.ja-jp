---
title: "(Macintosh オペレーティング システム) スタート パッドに最上位のカテゴリを追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ee2173c3-e464-4001-9f43-6d926a575092
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ae4eb5943d37b4a9d3b554af28cb425420782cf8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>(Macintosh オペレーティング システム) スタート パッドに最上位のカテゴリを追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Macintosh オペレーティング システムを実行しているコンピューター上のスタート パッドに最上位のカテゴリを追加することができます。 最上位のカテゴリを追加するスタート パッド アドインを作成するには、および使用方法の説明を」のトピックこのページからの情報の組み合わせを使用することができます追加のタスクとカテゴリのスタート パッドをですか?。[Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)します。  
  
 次の例は、.launchpad ファイルで最上位のカテゴリをスタート パッド エントリを指定する方法を示しています。  
  
```  
  
<?xml version="1.0" encoding="utf-8" ?>  
<LaunchPad resFile="Localizable">  
   <Category id="Microsoft.Launchpad.HomeCategory" name="SampleAddin"  image="SampleImage01.png">  
      <Task id="Microsoft.Launchpad.SampleAddin.Pictures"   
          name="Pictures"       
           src="smb://%ServerAddress%/Pictures"   
         image="SampleImage02.png"/>  
   </Category>  
</LaunchPad>  
```  
  
 最上位のカテゴリにするエントリ、カテゴリ要素の ID 属性が"microsoft.launchpad.homecategory"である必要があります。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)