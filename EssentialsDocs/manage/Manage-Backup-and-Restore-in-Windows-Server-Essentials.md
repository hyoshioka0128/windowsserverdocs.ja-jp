---
title: "バックアップを管理する windows Server Essentials と復元"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41000915-f6ff-4dbb-b7be-629ef36386d4
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6f6f0d27472664cd1cc538897d3d525fad506282
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="manage-backup-and-restore-in-windows-server-essentials"></a>バックアップを管理する windows Server Essentials と復元

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:
 
 Windows Server Essentials では、サーバーの定期的なバックアップと、ネットワーク コンピューターのバックアップを実行する信頼できる方法を提供します。 データの損失が発生した場合は、コンピューター全体を復元しなくても、サーバーに正常なバックアップからデータを復元できます。 必要に応じて、ネットワークで、サーバーまたはクライアント コンピューターにシステムの完全復元を実行できます。 次の表では、その利点と共に使用する別のバックアップのオプションについて説明します。  
  
|バックアップ機能|説明|利点|  
|--------------------|-----------------|----------------|  
|サーバーのバックアップ|Windows Server Essentials を実行しているサーバーをバックアップします。 データは外部 USB ドライブにバックアップします。<br /><br /> 詳細については、次を参照してください。[サーバー バックアップの管理](Manage-Server-Backup-in-Windows-Server-Essentials.md)と[の復元または修復サーバー](Restore-or-repair-your-server-running-Windows-Server-Essentials.md)します。|-サーバーのファイルとフォルダーを復元ことができます。<br /><br /> -サーバーの完全なシステム復元を実行できます。|  
|クライアント コンピューターのバックアップ|ネットワークのクライアント コンピューターをバックアップします。 データは、Windows Server Essentials を実行しているサーバーにバックアップされます。<br /><br /> 詳細については、次を参照してください。[クライアント バックアップの管理](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)と[既存のクライアント コンピューター バックアップから完全システムを復元](Restore-a-full-system-from-an-existing-client-computer-backup.md)します。|-サーバーからファイルとフォルダーを復元します。<br /><br /> -クライアント コンピューターのシステムの完全復元を実行できます。|  
| Microsoft Azure Backup|サーバー上のファイルまたはフォルダーのオンライン バックアップを実行します。 Azure Backup を使用してサーバー データをバックアップする場合は、情報がインターネット上のセキュリティで保護されたデータ センターにアップロードされる前に、パスフレーズを使用して暗号化されます。<br /><br /> 詳細については、次を参照してください。[オンライン バックアップの管理](Manage-Online-Backup-in-Windows-Server-Essentials.md)します。|-サーバーからファイルとフォルダーを復元します。<br /><br /> -、増分バックアップでは、ファイルへの変更のみがクラウドに転送されます。<br /><br /> -バックアップは、オンサイト バックアップ メディアを保護する負担が減ります Microsoft Azure とはのオフサイトに保管されます。|  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を使用します。](../use/Use-Windows-Server-Essentials.md)
