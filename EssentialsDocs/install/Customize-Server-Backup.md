---
title: サーバー バックアップのカスタマイズ
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19b2559c-6090-45af-9a08-2eefc28473c8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e7224ba49ecbf880dad8d88a2b197cc279e20d27
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311924"
---
# <a name="customize-server-backup"></a>サーバー バックアップのカスタマイズ

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

## <a name="turn-off-server-backup-by-default"></a>既定でのサーバー バックアップの無効化  
 サーバー バックアップを既定で無効にすることができます。 このオプションを有効にするには、**HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** の値を 1 に設定する必要があります。  
  
 このキーを設定すると、サーバー バックアップのユーザー インターフェイスは、ダッシュボードまたはスタート パッドを通じて公開されなくなります。 これにより、サーバー バックアップ用のサード パーティ アプリケーションを利用できます。  
  
#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>Serverbackupを追加するにはレジストリキーを指定し、値を1に設定します。  
  
1.  サーバー上で、 **[スタート]** ボタン、 **[ファイル名を指定して実行]** の順にクリックし、 **[名前]** ボックスに「**regedit**」と入力して、 **[OK]** をクリックします。  
  
2.  ナビゲーション ウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** 、 **[ServerBackup]** の順に展開します。  
  
3.  **[ServerBackup]** を右クリックして、 **[新規]** をクリックし、 **[DWORD 値]** をクリックします。  
  
4.  名前には、「**ProviderDisabled**」と入力します。  
  
5.  名前を右クリックして **[変更]** を選択し、値データに「**1**」と入力して **[OK]** をクリックします。  
  
## <a name="turn-on-server-backup"></a>サーバー バックアップの有効化  
 このドキュメントで前述した説明に従って **ProviderDisabled** レジストリ キーを作成してサーバー バックアップをオフにしている場合は、サーバー バックアップをオンにできます。  
  
 既定のサーバー バックアップを有効にするには、キー **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** を削除し、Windows Server Server Backup Service のサービス開始の種類を変更してサーバーを再起動する必要があります。  
  
#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>Serverbackup\ providerdisabled を削除しますか?レジストリキー  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、 **[検索]** をクリックします。  
  
2.  検索ボックスに「**regedit**」と入力して、 **[Regedit]** アプリケーションをクリックします。  
  
3.  ナビゲーション ウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** 、 **[ServerBackup]** の順に展開します。  
  
4.  **[ProviderDisabled]** を右クリックし、次に **[削除]** をクリックします。  
  
#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Windows Server Server Backup Service の開始の種類の変更  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、 **[検索]** をクリックします。  
  
2.  [検索] ボックスに「**services.msc**」と入力し、 **[サービス]** アプリケーションをクリックします。  
  
3.  サービス ウィンドウで、 **[Windows Server Server Backup Service]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[全般]** タブで、 **[スタートアップの種類]** として **[自動]** を選択します。  
  
5.  **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
#### <a name="restart-the-server"></a>サーバーの再起動  
  
1.  サーバーで、カーソルを画面の右上隅に移動して、**設定**、**電源**、再起動 の順にクリックします。