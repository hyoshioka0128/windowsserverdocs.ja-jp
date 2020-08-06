---
title: Windows Server Essentials でのリモート操作
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 8b183f8f-1279-4fdf-a495-c7c801563cb0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e2771abd6f59b81cd56a91bd2aeb7717c9093882
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838182"
---
# <a name="work-remotely-in-windows-server-essentials"></a>Windows Server Essentials でのリモート操作

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 Anywhere Access 機能 (リモート Web アクセス、仮想プライベート ネットワーク、DirectAccess) がサーバーで構成されている場合、ネットワークから離れているとき、さまざまな方法でサーバーにあるリソースにアクセスできます。

 次のトピックでは、離れた場所からサーバー リソースにアクセスする方法について説明しています。


-   [Windows Server Essentials でのリモート Web アクセスの使用](Work-Remotely-in-Windows-Server-Essentials.md#BKMA_RWA)

-   [VPN を利用した Windows Server Essentials への接続](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_3)

-   [My Server アプリを使用して Windows Server Essentials に接続する](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_App)

-   [Windows Phone 用に My Server を使用する](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_2)

-   [Windows Server Essentials と共に Microsoft Office 365 を利用する](Work-Remotely-in-Windows-Server-Essentials.md#BKMK_O365)

> [!NOTE]
>  サーバーで Anywhere Access を構成する方法の詳細については、「 [Anywhere access の管理](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)」を参照してください。

##  <a name="use-remote-web-access-in-windows-server-essentials"></a><a name="BKMA_RWA"></a>Windows Server Essentials でのリモート Web アクセスの使用

 リモート Web アクセスを利用すると、外出中も Windows Server Essentials ネットワークに接続された状態を維持できます。 詳細については、「[リモート Web アクセスを使用する](Use-Remote-Web-Access-in-Windows-Server-Essentials.md)」を参照してください。


##  <a name="use-vpn-to-connect-to-windows-server-essentials"></a><a name="BKMK_3"></a>VPN を使用して Windows Server Essentials に接続する
 Windows Server Essentials を実行しているホステッド サーバーに VPN 接続経由で接続するときに使用できるネットワーク アカウントでクライアント コンピューターを設定している場合、そのホステッド サーバーで新しく作成されたユーザー アカウントはすべて、初めてクライアント コンピューターにログオンするとき、VPN を使用する必要があります。 サーバーに接続されているクライアント コンピューターで、次の手順を完了します。

#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>VPN を利用して離れた場所からサーバー リソースにアクセスするには

1.  クライアント コンピューターで Ctrl + Alt + Del キーを押します。

2.  ログオン画面で **[ユーザーの切り替え]** をクリックします。

3.  画面右下隅にあるネットワーク ログオン アイコンをクリックします。

4.  ネットワーク ユーザー名とパスワードを利用し、Windows Server Essentials ネットワークにログオンします。

##  <a name="use-the-my-server-app-to-connect-to-windows-server-essentials"></a><a name="BKMK_App"></a>My Server アプリを使用して Windows Server Essentials に接続する
 My Server アプリを使用すると、windows ベースの PC、ノート pc、または Surface デバイスから、リソースに接続し、Windows Server Essentials サーバーの管理タスクを実行することができます。 サーバーで Windows Server 2012 が実行されている場合は、 [windows 用アプリ](https://windows.microsoft.com/windows-8/apps)から元の My server アプリをダウンロードします。 サーバーで Windows Server Essentials が実行されている場合は、代わりに My Server 2012 R2 アプリをダウンロードする必要があります。

 拡張 My Server 2012 R2 アプリを利用すると、リモート デスクトップからサーバーやクライアント コンピューターに接続できます。 Windows Server Essentials サーバーが Office 365 と統合されており、サブスクリプションに SharePoint Online が含まれている場合は、SharePoint Online ライブラリ内のドキュメントを操作して、My Server 2012 R2 から SharePoint チームサイトを開くこともできます。


 これらのアプリのインストールと使用の詳細については、「 [My Server アプリを使用する](Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)」を参照してください。

 これらのアプリのインストールと使用の詳細については、「 [My Server アプリを使用する](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)」を参照してください。


##  <a name="use-the-my-server-app-for-windows-phone"></a><a name="BKMK_2"></a>Windows Phone 用の My Server アプリの使用
 Windows Phone 用の My Server Windows アプリ (Windows Server 2012 の場合) および Windows Phone 用の My Server 2012 R2 アプリ (Windows Server Essentials の場合) は、リモートの場所で作業しているときにスマートフォンを使用してサーバーにシームレスに接続できるように設計されています。 これは、リモートアクセス用にサーバーを構成した後に Windows Server Essentials にアクセスするさまざまな方法の1つです。

 Windows Phone ストアからいずれかのアプリをダウンロードできます。

- [Windows Phone 用 My Server のインストール](http://www.windowsphone.com/store/app/my-server/6c2f98d5-6fcf-4e1d-b8b1-cde62ea1a94a)

- [Windows Phone 用 My Server 2012 R2 のインストール](http://www.windowsphone.com/store/app/my-server-2012-r2/44f596b5-0477-4096-b96e-ddd6ef64ad6b)

  My Server phone アプリの詳細については、ブログ記事「 [Windows Server Essentials 用の My server phone アプリ](/archive/blogs/sbs/my-server-phone-app-for-windows-server-2012-essentials)」を参照してください。 My Server 2012 R2 Phone アプリの詳細については、ブログ エントリの「 [My Server 2012 R2 Windows および Windows Phone アプリ](/archive/blogs/sbs/my-server-2012-r2-windows-and-windows-phone-apps)」を参照してください。

##  <a name="use-microsoft-office-365-with-windows-server-essentials"></a><a name="BKMK_O365"></a>Windows Server Essentials での Microsoft Office 365 の使用

 Office 365 は使い勝手の良い Web 対応ツールのセットです。これを利用すると、どこにいても、あらゆるデバイスから電子メール、重要なドキュメント、連絡先、カレンダーにアクセスできます。 詳細については、「[クイックスタートガイド Microsoft Office 365 を使用するに](Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)は」を参照してください。


## <a name="see-also"></a>関連項目

-   [Anywhere Access の管理](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [接続の取得](Get-Connected-in-Windows-Server-Essentials.md)

-   [共有フォルダーの使用](Use-Shared-Folders-in-Windows-Server-Essentials.md)

-   [デジタル メディアの再生](Play-Digital-Media-in-Windows-Server-Essentials.md)