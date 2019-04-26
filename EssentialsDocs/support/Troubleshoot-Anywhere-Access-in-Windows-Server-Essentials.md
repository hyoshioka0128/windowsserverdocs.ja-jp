---
title: Windows Server Essentials での Anywhere Access のトラブルシューティング
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68f2b05c-09eb-4cba-8db4-a91353b513c6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a14dbaed8c36f52814ba8080262ef60c399931dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874013"
---
# <a name="troubleshoot-anywhere-access-in-windows-server-essentials"></a>Windows Server Essentials での Anywhere Access のトラブルシューティング

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials で Anywhere Access の修復ウィザードを使用して、ネットワーク ユーザーがサーバー リソースにアクセスすることを妨げている問題のトラブルシューティングの一般的な手順を説明します。 リモート Web アクセス、仮想プライベート ネットワーク (VPN) の機能を任意の場所にアクセスし、DirectAccess は、任意のデバイスから、いつでも、インターネットに接続している任意の場所からサーバー リソースにアクセスするネットワーク ユーザーを有効にします。  
  
 Anywhere Access の修復ウィザードは、ネットワーク ユーザーがサーバー リソースにリモートでアクセスすることを妨げる、ルーター、ドメイン名、またはファイアウォールの問題を特定し、修復しようと試みます。  
  
> [!NOTE]
>  Windows Server Essentials コミュニティの最新のトラブルシューティング情報について、お勧めしますをご覧ください、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)します。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。  
  
### <a name="to-repair-anywhere-access"></a>Anywhere Access を修復するには  
  
1.  サーバーにログオンし、ダッシュボードを開きます。  
  
2.  **[設定]** をクリックし、 **[Anywhere Access]** タブをクリックします。  
  
3.  **[修復]** をクリックします。 Anywhere Access の修復ウィザードが起動します。  
  
4.  **[次へ]** をクリックします。 ウィザードは、Anywhere Access を分析し、問題を特定して、問題を修復しようと試みます。  
  
5.  ウィザードの完了時にアラートが表示される場合は、 **[再試行]** をクリックすると、問題の修復が再試行されます。 引き続きアラートが表示される場合は、アラートを確認して、問題に関する追加情報とトラブルシューティングの手順を参照します。  
  
### <a name="to-get-more-information-about-an-alert"></a>アラートに関する詳細情報を取得するには  
  
1.  ダッシュボードの右上隅の任意のエラーまたは警告アイコンをクリックして、アラート ビューアーを開きます。  
  
2.  アラート ビューアーで、エラーまたは警告をクリックして、追加情報を表示します。  
  
## <a name="additional-troubleshooting-for-anywhere-access"></a>Anywhere Access の追加のトラブルシューティング  
 Anywhere Access の修復ウィザードで Anywhere Access を修復できない場合は、次のトラブルシューティング リソースで、リモート Web アクセス、VPN、および DirectAccess に関する問題を確認します。  
  

-   [リモート Web アクセス接続をトラブルシューティングします。](Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [ファイアウォールをトラブルシューティングします。](Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  

-   [リモート Web アクセス接続をトラブルシューティングします。](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [ファイアウォールをトラブルシューティングします。](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  

  
-   チェック、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)Windows Server Essentials コミュニティによって報告された最新の問題。
