---
title: "サーバー バックアップをカスタマイズします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19b2559c-6090-45af-9a08-2eefc28473c8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d18dca276bccdf672664a5a3c2bd28e0221fff94
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="customize-server-backup"></a>サーバー バックアップをカスタマイズします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

## <a name="turn-off-server-backup-by-default"></a>既定ではサーバーのバックアップをオフにします。  
 既定では、サーバーのバックアップを無効にすることができます。 値を設定する必要があります**HKEY_LOCAL_MACHINE \software\microsoft\Windows Server \serverbackup\providerdisabled** 1 は、このオプションを有効にするためにします。  
  
 このキーが設定されている場合、サーバー バックアップのユーザー インターフェイスはダッシュ ボードまたはスタート パッドを通じて公開されません。 これにより、サーバー バックアップ用のサード パーティ製アプリケーションを利用することができます。  
  
#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>ServerBackup\ProviderDisabled を追加しますか。レジストリ キーと値を 1 に設定  
  
1.  サーバーで、をクリックして**開始**、] をクリックして**実行**、種類**regedit**で、**開く**textbox、] をクリックし、**[OK]**します。  
  
2.  ナビゲーション ウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**、し、展開**ServerBackup**します。  
  
3.  右クリック**ServerBackup**、] をクリックして**新規**、] をクリックし、**DWARD 値**します。  
  
4.  名前を入力して**ProviderDisabled**します。  
  
5.  名前を右クリックし、選択**変更**、入力**1**クリックして、値のデータの**OK**します。  
  
## <a name="turn-on-server-backup"></a>サーバーのバックアップを有効にします。  
 オンにするサーバーのバックアップを作成してオフになっていた場合**ProviderDisabled**レジストリ キー (このドキュメントで既に説明した)。  
  
 キーを削除する必要があります**HKEY_LOCAL_MACHINE \software\microsoft\Windows Server \serverbackup\providerdisabled**既定のサーバー バックアップを有効にする、Windows Server Server Backup Service のサービス開始の種類を変更し、サーバーを再起動するためにします。  
  
#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>ServerBackup\ProviderDisabled を削除しますか。レジストリ キー  
  
1.  サーバーで、マウスを移動して、画面の右上隅とクリックして**検索**します。  
  
2.  検索ボックスに次のように入力します。**regedit**、クリックして、**Regedit**アプリケーション。  
  
3.  ナビゲーション ウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**、し、展開**ServerBackup**します。  
  
4.  右クリック**ProviderDisabled**、] をクリックし、**削除**します。  
  
#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Windows Server Server Backup Service の開始の種類を変更します。  
  
1.  サーバーで、マウスを移動して、画面の右上隅とクリックして**検索**します。  
  
2.  検索ボックスに次のように入力します。**services.msc**、] をクリックし、**サービス**アプリケーション。  
  
3.  [サービス] ウィンドウで右クリックし、**Windows Server Server Backup Service**、] をクリック**プロパティ**します。  
  
4.  **全般**] タブで [**自動**の**スタートアップの種類**します。  
  
5.  をクリックして**OK**ダイアログ ボックスを閉じます。  
  
#### <a name="restart-the-server"></a>サーバーを再起動します  
  
1.  サーバーで、画面の右上隅にマウスを移動] をクリックして**設定**、] をクリックして**電源**、し、[再起動] をクリックします。