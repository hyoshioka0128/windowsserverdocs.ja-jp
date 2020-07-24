---
ms.assetid: bdb9ad4b-139c-4031-8f26-827432779829
title: ソリューションとシナリオ ガイド
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 02f0bb99b4948810c153bf1109ba4f04151b3030
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954194"
---
# <a name="solutions-and-scenario-guides"></a>ソリューションとシナリオ ガイド

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012
 
  
Microsoft のアクセスおよび情報保護ソリューションを使用すると、オンプレミス環境とクラウドアプリケーションの間で企業リソースへのアクセスをデプロイして構成することができます。 さらに、企業の情報を保護しながらこれを実現できます。  
  
アクセス保護と情報保護  
  
|ガイド|このガイドの使用方法                                                                                                                                                                                                                                                                                                                                                                                                    
|-----|-----  
| [任意の場所の任意のデバイスからの企業リソースへのセキュリティで保護されたアクセス](/previous-versions/windows/it-pro/solutions-guidance/dn550982(v=ws.11))|このガイドでは、従業員が個人および会社のデバイスを使用して、会社のアプリケーションやデータに安全にアクセスできるようにする方法について説明します。                                                                                                                                                                                    
| [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../ad-fs/operations/join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications.md) | 従業員は、任意のデバイスを使用してアプリケーションとデータにどこからでもアクセスできます。 さらに、ブラウザー アプリケーションや企業アプリケーションでシングル サインオンを使用できます。 管理者は、社内リソースにアクセスできるユーザーをアプリケーション、ユーザー、デバイス、および場所に基づいて制御できます。                                        
| [追加の多要素認証による個人情報アプリケーションのリスク管理](../ad-fs/operations/manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications.md)| このシナリオでは、特定のアプリケーションのユーザーのグループメンバーシップデータに基づいて MFA を有効にします。 つまり、特定のグループに属するユーザーが、Web サーバーでホストされている特定のアプリケーションへのアクセスを要求するときに、MFA を必須とするように、フェデレーション サーバーで認証ポリシーを設定します。  
| [条件付きアクセス制御によってリスクを管理する](../ad-fs/operations/manage-risk-with-conditional-access-control.md) | AD FS のアクセス制御は、発行承認要求規則を使用して実装されます。この規則は、ユーザーまたはユーザーグループが AD FS セキュリティで保護されたリソースにアクセスできるかどうかを決定する許可要求または拒否要求を発行するために使用されます。 承認規則は証明書利用者信頼を基づいてのみ設定できます。
|[カスタム ポート上で証明書キーベースの書き換え用の証明書の登録 Web サービスを構成する](certificate-enrollment-certificate-key-based-renewal.md)|この記事では、CEP および CES の自動更新機能を利用するための証明書キーベースの更新について、443以外のカスタムポートに証明書の登録 Web サービス (または証明書の登録ポリシー (CEP)/証明書登録サービス (CES) を実装する手順について説明します。 |
