---
title: 手順 4 OTP を使用した DirectAccess の検証
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 14d8a3a2138682fb552538948db604a75a1fe898
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858205"
---
# <a name="step-4-verify-directaccess-with-otp"></a>手順 4 OTP を使用した DirectAccess の検証

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、OTP 展開で DirectAccess が正しく構成されていることを確認する方法について説明します。
  
### <a name="to-verify-otp-health-on-the-remote-access-server"></a>リモートアクセスサーバーで OTP の正常性を確認するには

1. リモートアクセスサーバーで、**リモートアクセス管理**コンソールを開きます。  

2. **[リモートアクセスサーバー]** で、OTP をサポートするように構成されているリモートアクセスサーバーをクリックします。  

3. **[操作の状態]** をクリックします。  

4. OTP の状態に緑色のアイコンが表示され、動作していることを確認します。  
  
    > [!NOTE]  
    > 正常性状態の更新間隔は、レジストリキー HKLM\SYSTEM\CCS\Services\Ramgmtsvc\parameters\HealthRefreshTimeout からの値と、リモートアクセス構成で設定された**サーバーの利用状況の時間間隔**の最大値になります。  
  
### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>OTP 認証を使用して内部リソースへのアクセスを検証するには  
  
1.  DirectAccess クライアントコンピューターを企業ネットワークに接続し、コマンドプロンプトから**gpupdate/force**を実行して、グループポリシーを取得します。  
  
2.  クライアントコンピューターを企業ネットワークから切断し、外部ネットワークに接続して、内部リソースへのアクセスを試みます。 内部リソースにアクセスすることはできません。  
  
3.  ソフトウェアトークンの場合は、ベンダーの指示に従って OTP クライアントトークンにアクセスし、現在のトークンコードに注意してください。 ハードウェアトークンが使用されている場合は、ベンダーの指示に従って認証を行います。  
  
4.  通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。  
  
5.  **DirectAccess 接続**をクリックし、 **[続行]** をクリックします。  
  
6.  前にメモしたトークンコードを入力し、[ **OK]** をクリックします。 認証が完了するまで待ちます。 DirectAccess Workplace の接続状態が **接続**中 "になります。  
  
7.  内部リソースにアクセスしようとしました。 すべての企業リソースにアクセスできます。  
  


