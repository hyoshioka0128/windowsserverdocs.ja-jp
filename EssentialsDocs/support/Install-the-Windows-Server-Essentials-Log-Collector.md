---
title: Windows Server Essentials Log Collector のインストール
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d271c54f-1ffa-464e-afa5-27b8df61854e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ade18cec590392f35e7ad6b30d9a22ccdce44dcd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837033"
---
# <a name="install-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector のインストール

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials Log Collector のインストール ウィザードは、Log Collector をスタート パッド アドインとしてインストールします。 ネットワーク コンピューターまたはサーバー、またはその両方に Log Collector をインストールして使用できます。 インストールが完了したら、Log Collector がダッシュボードに表示されます。  
  
###  <a name="BKMK_ToInstall"></a> Log Collector をインストールするには  
  
1.  Log Collector インストール パッケージをネットワーク上の任意のサーバーまたはコンピューターにダウンロードします。  
  
    > [!NOTE]
    >  Microsoft から [Log Collector インストール パッケージをダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=255470) できます。  
  
2.  Log Collector のアイコンをダブルクリックします。  
  
3.  ネットワーク コンピューターからインストールを実行している場合は、指示に従い、サーバー管理者の資格情報を入力します。  
  
4.  マイクロソフト ソフトウェア ライセンス条項に同意することを選択します。  
  
5.  サーバーにのみ Log Collector をインストールするには、**[サーバーのみ]** チェック ボックスをオンにします。 すべてのネットワーク コンピューターに Log Collector をインストールするには、**[サーバー、およびネットワーク上のすべてのコンピューター]** チェック ボックスをオンにします。  
  
6.  **[アドインのインストール]** をクリックします。  
  
###  <a name="BKMK_Reinstall"></a> Log Collector を再インストールします。  
 Log Collector を再インストールする必要がある場合は、サーバーおよびネットワーク コンピューター上の Log Collector をアンインストールして、再インストールする必要があります。 ダッシュボードからサーバー上の Log Collector をアンインストールすると、すべてのネットワーク コンピューターで自動的に Log Collector がアンインストールされます。  
  
##### <a name="to-uninstall-and-reinstall-the-log-collector"></a>Log Collector をアンインストールおよび再インストールするには  
  
1.  ダッシュボードを開きます。  
  
2.  **[アドイン]** タブをクリックし、一覧から **[Log Collector]** を選択して、**[アンインストール]** をクリックします。  
  

3.  前述の「 [To install the Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall)」にある手順を実行し、Log Collector をダウンロードしてインストールします。  

3.  前述の「 [To install the Log Collector](../support/Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall)」にある手順を実行し、Log Collector をダウンロードしてインストールします。  

  
### <a name="manually-install-the-log-collector"></a>Log Collector を手動でインストールする  
 インストール ウィザードで Log Collector のインストールに失敗した場合、次の手順を使用して、Log Collector を 1 つのコンピューターにインストールできます。  
  
##### <a name="to-manually-install-the-log-collector"></a>Log Collector を手動でインストールするには  
  
1.  .Cab に .wssx からダウンロードしたインストール ファイルの拡張子の名前を変更します。  
  
2.  インストール ファイルの名前をダブルクリックします。  
  
3.  指示が表示されたら、**[OK]** をクリックします。  
  
4.  ˜.msi で終わるファイル名をダブルクリックし、展開先のフォルダーを選択します。  
  
5.  ファイルを展開したフォルダーに移動して、インストール ファイルをダブルクリックし、ウィザードを使用してインストールを完了します。
