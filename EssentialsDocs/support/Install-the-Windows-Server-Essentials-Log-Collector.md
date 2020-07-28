---
title: Windows Server Essentials Log Collector のインストール
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: d271c54f-1ffa-464e-afa5-27b8df61854e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ead1f75ce459523fbb2678ed369949f679fb3124
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180368"
---
# <a name="install-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector のインストール

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials Log Collector のインストールウィザードでは、Log Collector がスタートパッドアドインとしてインストールされます。 ネットワーク コンピューターまたはサーバー、またはその両方に Log Collector をインストールして使用できます。 インストールが完了したら、Log Collector がダッシュボードに表示されます。

###  <a name="to-install-the-log-collector"></a><a name="BKMK_ToInstall"></a>Log Collector をインストールするには

1.  Log Collector インストール パッケージをネットワーク上の任意のサーバーまたはコンピューターにダウンロードします。

    > [!NOTE]
    > [Windows Server Essentials Log Collector インストールパッケージをダウンロード](https://www.microsoft.com/download/details.aspx?id=34821)します。

2.  Log Collector のアイコンをダブルクリックします。

3.  ネットワーク コンピューターからインストールを実行している場合は、指示に従い、サーバー管理者の資格情報を入力します。

4.  マイクロソフト ソフトウェア ライセンス条項に同意することを選択します。

5.  サーバーにのみ Log Collector をインストールするには、[**サーバーのみ**] チェック ボックスをオンにします。 すべてのネットワーク コンピューターに Log Collector をインストールするには、[**サーバー、およびネットワーク上のすべてのコンピューター**] チェック ボックスをオンにします。

6.  [**アドインのインストール**] をクリックします。

###  <a name="reinstalling-the-log-collector"></a><a name="BKMK_Reinstall"></a>Log Collector を再インストールしています
 Log Collector を再インストールする必要がある場合は、サーバーおよびネットワーク コンピューター上の Log Collector をアンインストールして、再インストールする必要があります。 ダッシュボードからサーバー上の Log Collector をアンインストールすると、すべてのネットワーク コンピューターで自動的に Log Collector がアンインストールされます。

##### <a name="to-uninstall-and-reinstall-the-log-collector"></a>Log Collector をアンインストールおよび再インストールするには

1.  ダッシュボードを開きます。

2.  [**アドイン**] タブをクリックし、一覧から [**Log Collector**] を選択して、[**アンインストール**] をクリックします。

3.  前の手順「[Log Collector をインストールするには](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_ToInstall)」にある手順を実行し、Log Collector をダウンロードしてインストールします。

### <a name="manually-install-the-log-collector"></a>Log Collector を手動でインストールする
 インストール ウィザードで Log Collector のインストールに失敗した場合、次の手順を使用して、Log Collector を 1 つのコンピューターにインストールできます。

##### <a name="to-manually-install-the-log-collector"></a>Log Collector を手動でインストールするには

1.  ダウンロードしたインストールファイルの拡張子を、. wssx から .cab に変更します。

2.  インストール ファイルの名前をダブルクリックします。

3.  指示が表示されたら、[**OK**] をクリックします。

4.  ' .Msi ' で終わるファイル名をダブルクリックし、展開先のフォルダーを選択します。

5.  ファイルを展開したフォルダーに移動して、インストール ファイルをダブルクリックし、ウィザードを使用してインストールを完了します。
