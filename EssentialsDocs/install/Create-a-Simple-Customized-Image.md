---
title: 単純なカスタマイズ イメージの作成
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 74a1729f9445710b6b9d279f1603295eff2a5d25
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312136"
---
# <a name="create-a-simple-customized-image"></a>単純なカスタマイズ イメージの作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

簡単なカスタマイズされたイメージを作成するために、以下の手順を使用できます。  
  
#### <a name="to-create-the-image"></a>イメージを作成するには  
  
1.  サーバーのインストール後、初期構成の最初のページで、Shift キーを押しながら F10 を押してコマンド プロンプト ウィンドウを起動します。  
  
2.  システム ドライブのルートの下に SkipIC.txt ファイルを作成します。  
  
3.  サーバーを再起動します。  
  
4.  unattend.xml ファイルを保存している USB フラッシュ ドライブまたは DVD を使用して、サーバーを起動します。 ブート可能な USB フラッシュ ドライブの作成の詳細については、「[ブート可能な USB フラッシュ ドライブの作成](Create-a-Bootable-USB-Flash-Drive.md)」を参照してください。  
  
5.  ロゴ ブランドをダッシュボードに追加します。 ブランドの追加の詳細については、「[ダッシュボード、リモート Web アクセス、スタート パッドへのブランドの追加](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md)」を参照してください。  
  
6.  会社名、ロゴ、EULA などのカスタム情報を表示するために OOBE.xml ファイルを作成します。 OOBE.xml ファイルの詳細については、「 [Create the Oobe.xml File Including Logo and EULA](Create-the-Oobe.xml-File-Including-Logo-and-EULA.md)」を参照してください。  
  
7.  unattend.xml で既定のサーバー名を定義しない場合は、その名前を変更します。  
  
8.  既定では、サーバー名はランダムな文字列です。 サーバー名を ContosoServer などの別の文字列に変更して、その新しいサーバー名を顧客に通知します。  
  
9. 「[イメージの展開の準備](Preparing-the-Image-for-Deployment.md)」の説明に従ってイメージの展開を準備します。  
  
## <a name="see-also"></a>参照  
 [Windows Server ESSENTIALS ADK でのはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)