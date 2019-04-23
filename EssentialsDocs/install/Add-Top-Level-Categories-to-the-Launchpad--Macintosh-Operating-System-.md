---
title: 最上位のカテゴリをスタートパッドに追加する (Macintosh オペレーティング システム)
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869963"
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>最上位のカテゴリをスタートパッドに追加する (Macintosh オペレーティング システム)

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Macintosh オペレーティン グシステムを実行しているコンピューター上のスタート パッドに最上位のカテゴリを追加できます。 最上位のカテゴリを追加するスタート パッド アドインを作成するには、このページおよび」に関する「方法」トピックからの情報の組み合わせを使用できます。 しますタスクとカテゴリをスタート パッドに追加しますか。[Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648)します。  
  
 次の例は、.launchpad ファイルで最上位のカテゴリにするスタートパッド エントリを指定する方法を示します。  
  
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
  
 エントリを最上位のカテゴリにするには、カテゴリ要素の Id 属性が "Microsoft.Launchpad.HomeCategory" でなければなりません。  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)