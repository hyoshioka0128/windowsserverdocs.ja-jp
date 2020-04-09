---
title: 手順 2 RADIUS サーバーの展開を計画する
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 2d6ad863-02a5-49b0-9aff-d189e78b2b80
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1722b750405ea1188d18fab6282d82434f5334ef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858175"
---
# <a name="step-2-plan-the-radius-server-deployment"></a>手順 2 RADIUS サーバーの展開を計画する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

単一のリモートアクセスサーバーを展開した後、ワンタイムパスワード (OTP) 認証サーバーを計画します。  
  
|タスク|説明|  
|----|--------|  
|2.1 RADIUS サーバーを計画する|OTP 認証サーバーでは、Windows Server 2016 および Windows Server 2012 のリモートアクセスで、パスワード認証プロトコル (PAP) をサポートするすべての RADIUS 対応 OTP サーバーがサポートされます。|  
  
## <a name="21-plan-the-radius-server"></a><a name="BKMK_1.1"></a>2.1 RADIUS サーバーを計画する  
OTP 認証用に RADIUS サーバーを計画するときは、次の点に注意してください。  
  
-   ほとんどの種類の OTP 展開では、リモートアクセスサーバーを RADIUS エージェントとして構成する必要があります。 詳細については、OTP ベンダのドキュメントを参照してください。  
  
-   すべての OTP 展開では、Active Directory ユーザーを RADIUS サーバーと同期する必要があります。  
  
-   RADIUS サーバーはドメインメンバーである必要はありません。  
  
-   RADIUS サーバーを展開するときに、RADIUS トラフィックの共有シークレットとポート番号を構成します。 これらの詳細をメモしておきます。リモートアクセスサーバーを構成するときに必要になります。  
  
[「Otp 認証と Rsa securid を使用した DirectAccess のデモンストレーション」の「テストラボガイド](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/tlg-otp-securid/test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid)」で、RSA securid サーバーで otp 認証を設定するテストラボガイドの例を見ることができます。  
  
  
  


