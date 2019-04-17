---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: "AD DS の所有者の役割用の DNS の割り当てください。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e393cbf32aa5a13ff22044eabb8c575508baaf79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>AD DS の所有者の役割用の DNS の割り当てください。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォレストの所有者には、フォレストの Active Directory ドメイン サービス (AD DS) の所有者のドメイン ネーム システム (DNS) が割り当てられます。 フォレストの AD DS の所有者の DNS は、ユーザー (またはユーザーのグループ) だれが監督 DNS の展開を担当するドメイン名が適切なインターネット機関に登録されていることを確認する (必要な場合)、AD DS インフラストラクチャをします。  
  
AD DS の所有者の DNS は、DNS で、フォレストの AD DS の設計を担当します。 組織は、DNS サーバー サービスを動作している場合、既存の DNS サーバー サービスの DNS デザイナーは、フォレスト ルート DNS 名をドメイン コントローラーで実行されている DNS サーバーを委任する AD DS の所有者の DNS で動作します。  
  
フォレストの AD DS の所有者の DNS はまた、動的ホスト構成プロトコル (DHCP) とグループ、組織内の DNS のグループとの連絡先を維持し、これらのグループとの間、フォレスト内の各ドメインの個々 の DNS の所有者の計画 (ある場合) を調整します。 フォレストの DNS の所有者は、各グループは、DNS の設計計画の認識と早い段階の入力を提供できるように、DHCP と DNS のグループが AD DS 設計プロセスの DNS に関係することを確認します。  
  


