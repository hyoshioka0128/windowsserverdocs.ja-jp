---
title: 手順4リモートアクセスサーバーで OTP を計画する
description: このトピックは、「Windows Server 2016 で OTP 認証を使用してリモートアクセスを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4b97b2fd-767a-45c1-a64e-5b3edd0c8a47
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 789fd72e2f3fc1693bf4803f33dcc1e7f1b3acc3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855775"
---
# <a name="step-4-plan-for-otp-on-the-remote-access-server"></a>手順4リモートアクセスサーバーで OTP を計画する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ワンタイムパスワード (OTP) の RADIUS サーバーと証明書の設定を計画した後、リモートアクセス OTP の展開を計画するための最後の手順は、リモートアクセスサーバーでのクライアント OTP 設定を計画することです。  
  
|タスク|説明|  
|----|--------|  
|[4.1 OTP クライアントの除外を計画する](#bkmk_4_1_Exemptions)|OTP を使用した認証を必要としないユーザーの除外を計画します。|  
|[4.2 Windows 7 クライアントの計画](#bkmk_4_2_Win7)|DirectAccess Connectivity Assistant (DCA) 2.0 を Windows 7 クライアントコンピューターに展開することを計画します。|  
|[4.3 スマートカードの計画](#BKMK_smartcard)|追加の承認にスマートカードを使用することを計画します。|  
  
## <a name="41-plan-for-otp-client-exemptions"></a><a name="bkmk_4_1_Exemptions"></a>4.1 OTP クライアントの除外を計画する  
OTP 認証が有効になっている場合、既定では、ユーザー名とパスワード、および OTP 資格情報の組み合わせを使用して認証する必要があります。 ただし、選択したユーザーに対して、ユーザー名とパスワードのみを使用した認証を許可することができます (OTP は不要)。 これを行うには、セキュリティグループを作成し、OTP 認証から除外するユーザーを追加します。  
  
> [!NOTE]  
> クライアントの除外対象として選択できるセキュリティグループは1つだけであるため、1つのフォレストのクライアントコンピューターのみを除外することができます。  
  
## <a name="42-plan-for-windows-7-clients"></a><a name="bkmk_4_2_Win7"></a>4.2 Windows 7 クライアントの計画  
既定では、Windows 7 クライアントコンピューターは OTP を使用した認証を行うことができません。  Windows 7 クライアントコンピューターでは、Windows Server 2012 リモートアクセス展開で OTP を使用して認証を行うには、DCA 2.0 が必要です。 DCA 2.0 の詳細については、Microsoft ダウンロードセンターの「 [DirectAccess Connectivity Assistant 2.0](https://go.microsoft.com/fwlink/?LinkId=253699) 」を参照してください。  
  
## <a name="43-plan-for-smart-cards"></a><a name="BKMK_smartcard"></a>4.3 スマートカードの計画  
OTP 認証が有効になっている場合、追加の承認にスマートカードを使用できるようにするオプションがあります。 ユーザーのスマートカードが機能していない場合に、一時的なアクセスを許可するセキュリティグループを作成します。  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目  
  
-   [OTP 認証を使用して DirectAccess を構成する](https://technet.microsoft.com/windows-server-docs/networking/remote-access/ras/otp/deploy-ra-otp)  
  


