---
title: Windows Server Essentials Log Collector のインストール
description: Windows Server Essentials の使用方法について説明します。
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
ms.openlocfilehash: a1b1a5492a6e5dbc48899b3918314676884e0454
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322094"
---
# <a name="install-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector のインストール

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials Log Collector のインストールウィザードでは、Log Collector がスタートパッドアドインとしてインストールされます。 ネットワーク コンピューターまたはサーバー、またはその両方に Log Collector をインストールして使用できます。 インストールが完了したら、Log Collector がダッシュボードに表示されます。  
  
###  <a name="BKMK_ToInstall"></a>Log Collector をインストールするには  
  
1.  Log Collector インストール パッケージをネットワーク上の任意のサーバーまたはコンピューターにダウンロードします。  
  
    > [!NOTE]
    > [Windows Server Essentials Log Collector インストールパッケージをダウンロード](https://www.microsoft.com/download/details.aspx?id=34821)します。  
  
2.  Log Collector のアイコンをダブルクリックします。  
  
3.  ネットワーク コンピューターからインストールを実行している場合は、指示に従い、サーバー管理者の資格情報を入力します。  
  
4.  マイクロソフト ソフトウェア ライセンス条項に同意することを選択します。  
  
5.  サーバーにのみ Log Collector をインストールするには、 **[サーバーのみ]** チェック ボックスをオンにします。 すべてのネットワーク コンピューターに Log Collector をインストールするには、 **[サーバー、およびネットワーク上のすべてのコンピューター]** チェック ボックスをオンにします。  
  
6.  **[アドインのインストール]** をクリックします。  
  
###  <a name="BKMK_Reinstall"></a>Log Collector を再インストールしています  
 Log Collector を再インストールする必要がある場合は、サーバーおよびネットワーク コンピューター上の Log Collector をアンインストールして、再インストールする必要があります。 ダッシュボードからサーバー上の Log Collector をアンインストールすると、すべてのネットワーク コンピューターで自動的に Log Collector がアンインストールされます。  
  
##### <a name="to-uninstall-and-reinstall-the-log-collector"></a>Log Collector をアンインストールおよび再インストールするには  
  
1.  [ダッシュボード] を開きます。  
  
2.  **[アドイン]** タブをクリックし、一覧から **[Log Collector]** を選択して、 **[アンインストール]** をクリックします。  
  

3.  前の手順「[Log Collector をインストールするには](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall)」にある手順を実行し、Log Collector をダウンロードしてインストールします。  

3.  前の手順「[Log Collector をインストールするには](../support/Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall)」にある手順を実行し、Log Collector をダウンロードしてインストールします。  

  
### <a name="manually-install-the-log-collector"></a>Log Collector を手動でインストールする  
 インストール ウィザードで Log Collector のインストールに失敗した場合、次の手順を使用して、Log Collector を 1 つのコンピューターにインストールできます。  
  
##### <a name="to-manually-install-the-log-collector"></a>Log Collector を手動でインストールするには  
  
1.  ダウンロードしたインストールファイルの拡張子を、. wssx から .cab に変更します。  
  
2.  インストール ファイルの名前をダブルクリックします。  
  
3.  指示が表示されたら、 **[OK]** をクリックします。  
  
4.  ' .Msi ' で終わるファイル名をダブルクリックし、展開先のフォルダーを選択します。  
  
5.  ファイルを展開したフォルダーに移動して、インストール ファイルをダブルクリックし、ウィザードを使用してインストールを完了します。
