---
title: Windows Server Essentials での Anywhere Access のトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 68f2b05c-09eb-4cba-8db4-a91353b513c6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9ebb4f27201e7cdb8e412bc35b217185616df3cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852255"
---
# <a name="troubleshoot-anywhere-access-in-windows-server-essentials"></a>Windows Server Essentials での Anywhere Access のトラブルシューティング

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials の Anywhere Access の修復ウィザードを使用して、ネットワークユーザーがサーバーリソースにアクセスできない問題のトラブルシューティングを行うための一般的な手順について説明します。 Anywhere Access の機能-リモート Web アクセス、仮想プライベートネットワーク (VPN)、および DirectAccess-ネットワークユーザーは、任意のデバイスから、いつでもインターネット接続を使用して、任意の場所からサーバーリソースにアクセスできます。  
  
 Anywhere Access の修復ウィザードは、ネットワーク ユーザーがサーバー リソースにリモートでアクセスすることを妨げる、ルーター、ドメイン名、またはファイアウォールの問題を特定し、修復しようと試みます。  
  
> [!NOTE]
>  Windows Server Essentials コミュニティの最新のトラブルシューティング情報については、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)を参照することをお勧めします。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。  
  
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
  

-   [リモート Web アクセス接続のトラブルシューティング](Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [ファイアウォールのトラブルシューティング](Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  

-   [リモート Web アクセス接続のトラブルシューティング](../support/Troubleshoot-Remote-Web-Access-connectivity-in-Windows-Server-Essentials.md)  
  
-   [ファイアウォールのトラブルシューティング](../support/Troubleshoot-your-firewall-in-Windows-Server-Essentials.md)  

  
-   Windows server essentials コミュニティによって報告された最新の問題については、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/winserveressentials/threads)をご覧ください。
