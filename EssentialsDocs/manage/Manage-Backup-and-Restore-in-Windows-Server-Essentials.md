---
title: Windows Server Essentials でのバックアップと復元の管理
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828523"
---
# <a name="manage-backup-and-restore-in-windows-server-essentials"></a>Windows Server Essentials でのバックアップと復元の管理

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials
 
 Windows Server Essentials を導入すれば、信頼できる方法でサーバーの通常バックアップとネットワーク コンピューターのバックアップを実行できます。 データが失われた場合、コンピューター全体を復元しなくても、サーバーのバックアップからデータを復元できます。 必要であれば、システム全体をネットワークにあるサーバーまたはクライアント コンピューターに復元できます。 次の表は、利用できるさまざまなバックアップ オプションとその長所をまとめたものです。  
  
|バックアップ機能|説明|長所|  
|--------------------|-----------------|----------------|  
|サーバー バックアップ|Windows Server Essentials を実行しているサーバーをバックアップします。 データは外部 USB ドライブにバックアップされます。<br /><br /> 詳細については、次を参照してください。 [Manage Server Backup](Manage-Server-Backup-in-Windows-Server-Essentials.md)と[復元または修復サーバー](Restore-or-repair-your-server-running-Windows-Server-Essentials.md)します。|-サーバーのファイルとフォルダーを復元するできます。<br /><br /> -サーバーの完全システム復元を実行するできます。|  
|クライアント コンピューター バックアップ|ネットワークのクライアント コンピューターをバックアップします。 データは Windows Server Essentials を実行しているサーバーにバックアップされます。<br /><br /> 詳細については、次を参照してください。[クライアント バックアップの管理](Manage-Client-Computer-Backup-in-Windows-Server-Essentials.md)と[、完全なシステムを既存のクライアント コンピューター バックアップから復元](Restore-a-full-system-from-an-existing-client-computer-backup.md)します。|-サーバーからファイルとフォルダーを復元することができます。<br /><br /> -クライアント コンピューターの完全システム復元を実行します。|  
| Microsoft Azure Backup|サーバーのファイルまたはフォルダーのオンライン バックアップを実行します。 Azure Backup を使用してサーバー データをバックアップする場合は、情報がインターネット上のセキュリティで保護されたデータ センターにアップロードされる前に、パスフレーズを使用して暗号化されます。<br /><br /> 詳細については、次を参照してください。[オンライン バックアップの管理](Manage-Online-Backup-in-Windows-Server-Essentials.md)します。|-サーバーからファイルとフォルダーを復元することができます。<br /><br /> -増分バックアップでは、ファイルへの変更のみが、クラウドに転送されます。<br /><br /> のオンサイト バックアップ メディアを保護する必要性を減らすことの Microsoft Azure とのオフサイトでバックアップが格納されます。|  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を使用します。](../use/Use-Windows-Server-Essentials.md)
