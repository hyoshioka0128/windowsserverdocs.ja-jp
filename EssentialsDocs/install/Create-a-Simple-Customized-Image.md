---
title: 単純なカスタマイズ イメージの作成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 29f9a09f-e4e8-476d-ada1-ab9202a670d7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8e2d4b20de9cee6617ab5b0f32b161eab3bc4a8e
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181398"
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
 [Windows Server ESSENTIALS ADK を使用したはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)[イメージの作成とカスタマイズ追加の](Creating-and-Customizing-the-Image.md)[カスタマイズカスタマイズ](Additional-Customizations.md)[のイメージの準備カスタマーエクスペリエンスをテストするためのイメージの準備](Preparing-the-Image-for-Deployment.md) [Testing the Customer Experience](Testing-the-Customer-Experience.md)