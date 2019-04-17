---
title: "単純なカスタマイズ イメージを作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e18ff5ded94127449072d28d00b98e17dbe63c3a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-simple-customized-image"></a>単純なカスタマイズ イメージを作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

単純なカスタマイズ イメージを作成するため、次の手順を使用することができます。  
  
#### <a name="to-create-the-image"></a>イメージを作成するには  
  
1.  サーバーのインストール後の初期構成は、最初のページで、コマンド プロンプト ウィンドウを起動する shift キーを押しながら f10 を押してキーを押します。  
  
2.  システム ドライブのルートの下にある SkipIC.txt ファイルを作成します。  
  
3.  サーバーを再起動します。  
  
4.  USB フラッシュ ドライブまたは unattend.xml ファイルを含む、DVD を使用して、サーバーを起動します。 起動可能な USB フラッシュ ドライブを作成する方法の詳細については、次を参照してください。[起動可能な USB フラッシュ ドライブを作成する](Create-a-Bootable-USB-Flash-Drive.md)します。  
  
5.  ダッシュ ボードへのロゴ ブランドを追加します。 ブランドの追加に関する詳細については、次を参照してください。[ダッシュ ボード、リモート Web アクセス、スタート パッドへのブランドの追加](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md)します。  
  
6.  会社名、ロゴ、EULA などのカスタム情報を表示する、OOBE.xml ファイルを作成します。 OOBE.xml ファイルの詳細については、次を参照してください。[Oobe.xml ファイルを含むロゴおよび EULA を作成する](Create-the-Oobe.xml-File-Including-Logo-and-EULA.md)します。  
  
7.  Unattend.xml で定義しない場合は、既定のサーバー名を変更します。  
  
8.  既定では、サーバー名をランダムな文字列となります。 (ContosoServer などの別の文字列に、サーバーの名前を変更し、新しいサーバー名についてお客様に通知します。  
  
9. 展開のイメージを準備する」の説明に従って[イメージの展開の準備](Preparing-the-Image-for-Deployment.md)します。  
  
## <a name="see-also"></a>参照してください。  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)