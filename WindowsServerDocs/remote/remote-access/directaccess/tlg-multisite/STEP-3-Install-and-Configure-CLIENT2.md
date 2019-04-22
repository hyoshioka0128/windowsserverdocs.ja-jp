---
title: 手順 3 のインストールおよび CLIENT2 の構成
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f009fdd1-94e6-4ccb-8c6e-609a5394db53
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d19f204e139433d11cf674c4ec39a134cde7eefa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813173"
---
# <a name="step-3-install-and-configure-client2"></a>手順 3 のインストールおよび CLIENT2 の構成

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

CLIENT2 は、Windows 7&reg;を示すために使用するコンピューター、旧バージョンと Windows Server 2016 サーバーで実行されているリモート アクセスの互換性。  
  
1. Client2 オペレーティング システムをインストールします。 Windows のインストール&reg;7 Enterprise または Windows&reg; client2 7 Ultimate。  
  
2. CLIENT2 を CORP ドメインに参加。 CLIENT2 を corp.contoso.com ドメインに参加させます。  
  
## <a name="to-install-the-operating-system-on-client2"></a>CLIENT2 で、オペレーティング システムをインストールするには  
  
1.  Windows 7 のインストールを開始します。  
  
2.  ユーザー名を求められたら、入力**User1**します。 コンピューター名を求められたら、入力**CLIENT2**します。  
  
3.  パスワードを求められたら、強力なパスワードを 2 回入力します。  
  
4.  保護設定のダイアログ ボックスが表示されたら、クリックして**推奨設定を使用**します。  
  
5.  コンピューターの現在の場所のダイアログ ボックスが表示されたら、クリックして**作業ネットワーク**します。  
  
6.  CLIENT2 をインターネットにアクセスできるネットワークに接続し、Windows 7 では、最新の更新プログラムをインストールし、インターネットから切断し、Windows Update を実行します。  
  
7.  CLIENT2 を Corpnet サブネットに接続します。  
  
## <a name="user-account-control"></a>ユーザー アカウント制御  
Windows 7 オペレーティング システムを構成する場合は、をクリックする必要が**続行**上、**ユーザー アカウント制御**一部のタスク (UAC) ダイアログ ボックス。 いくつかの構成タスクには、UAC の承認が必要です。 メッセージが表示されたら、いつでもクリックして**続行**これらの変更を承認します。  
  
## <a name="to-join-client2-to-the-corp-domain"></a>CLIENT2 を CORP ドメインに参加させる  
  
1.  **[スタート]** ボタンをクリックし、 **[コンピューター]** を右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **システム**] ページの [、**コンピューター名、ドメインおよびワークグループの設定**領域で、をクリックして**設定を変更する**します。  
  
3.  **[システムのプロパティ]** ダイアログ ボックスの **[コンピューター名]** タブで **[変更]** をクリックします。  
  
4.  **コンピューター名/ドメイン名の変更**ダイアログ ボックスで、をクリックして**ドメイン**、型**corp.contoso.com**、順にクリックします **[ok]** します。  
  
5.  ユーザー名とパスワードを求められたら、ユーザー名と、User1 のドメイン アカウントのパスワードを入力し、 **OK**します。  
  
6.  corp.contoso.com ドメインへの参加を知らせるダイアログ ボックスが表示されたら、**[OK]** をクリックします。  
  
7.  コンピューターを再起動し、をクリックすることを求めるダイアログ ボックスが表示されたら**OK**します。  
  
8.  **システム プロパティ**ダイアログ ボックスで、をクリックして**閉じる**とコンピューターを再起動し、をクリックするよう求めるダイアログを表示する**今すぐ再起動**します。  
  
9. コンピューターの再起動後に、corp \user1 としてログオンします。
