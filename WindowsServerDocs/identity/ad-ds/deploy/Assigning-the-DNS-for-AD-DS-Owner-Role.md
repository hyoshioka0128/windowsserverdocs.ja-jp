---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: AD DS の DNS の所有者の役割を割り当てる
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dde9ed6035b30ba5b5b96b7132d25a1f8a1c0b8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884023"
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>AD DS の DNS の所有者の役割を割り当てる

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

フォレストの所有者には、フォレストの Active Directory Domain Services (AD DS) の所有者のドメイン ネーム システム (DNS) が割り当てられます。 DNS フォレストの AD DS の所有者では、ユーザー (またはユーザーのグループ)、DNS の展開の監視を担当するユーザー ドメイン名が適切なインターネット機関に登録されていることを確認する (必要な) 場合、AD DS インフラストラクチャ。  
  
AD DS の所有者の DNS は、DNS で、フォレストの AD DS の設計を担当します。 組織は、DNS サーバー サービスを動作している場合、既存の DNS サーバー サービスの DNS のデザイナーは、AD DS の所有者のドメイン コント ローラーで実行されている DNS サーバーには、フォレスト ルート DNS 名をデリゲートに DNS で動作します。  
  
DNS フォレストの AD DS の所有者では、動的ホスト構成プロトコル (DHCP) のグループと組織の DNS のグループにお問い合わせくださいが保持され、これらのグループと各ドメイン、フォレスト内の個々 の DNS 所有者のプラン (ある場合) を調整します。 フォレストの DNS 所有者によりように DNS の設計計画の対応は、各グループと初期入力を提供することができます、DHCP および DNS のグループが AD DS 設計プロセスの DNS に関与しているようになります。  
  


