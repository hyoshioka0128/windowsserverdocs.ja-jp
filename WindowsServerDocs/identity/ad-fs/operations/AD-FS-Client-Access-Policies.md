---
ms.assetid: ''
title: AD FS のクライアント Access Control ポリシー
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c00a13076b3c3cf28f9efa0a5127f50e34219c84
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358633"
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Active Directory フェデレーションサービス (AD FS) を使用して組織のデータへのアクセスを制御する

このドキュメントでは、オンプレミス、ハイブリッド、クラウドの各シナリオでの AD FS によるアクセス制御の概要について説明します。  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>オンプレミスのリソースへの AD FS と条件付きアクセス 
Active Directory フェデレーションサービス (AD FS) が導入されたため、承認ポリシーを使用して、要求とリソースの属性に基づいてリソースへのアクセスを制限または許可することができました。  AD FS がバージョンからバージョンに移行すると、これらのポリシーの実装方法が変更されました。  バージョン別のアクセス制御機能の詳細については、次を参照してください。
- [Windows Server 2016 の AD FS の Access Control ポリシー](Access-Control-Policies-in-AD-FS.md)
- [Windows Server 2012 R2 の AD FS でのアクセス制御](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>ハイブリッド組織での AD FS と条件付きアクセス  

AD FS には、ハイブリッドシナリオでの条件付きアクセスポリシーのオンプレミスコンポーネントが用意されています。 AD FS ベースの承認規則は、AD FS に直接フェデレーションされるオンプレミスアプリケーションなど、Azure AD 以外のリソースに対して使用する必要があります。  クラウドコンポーネントは[Azure AD 条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)によって提供されます。  Azure AD Connect は、2つのコントロールプレーンを接続します。

たとえば、クラウドリソースへの条件付きアクセスのために Azure AD にデバイスを登録すると、Azure AD Connect デバイスの書き戻し機能によって、デバイスの登録情報がオンプレミスで使用可能になり AD FS ポリシーが使用および適用されます。  これにより、内部設置型の両方のアクセス制御ポリシーと、クラウド リソースを一貫した方法があります。  

![条件付きアクセス](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Office 365 用のクライアントアクセスポリシーの進化
多くのユーザーは AD FS でクライアントアクセスポリシーを使用して、クライアントの場所や使用されているクライアントアプリケーションの種類などの要因に基づいて、Office 365 およびその他の Microsoft オンラインサービスへのアクセスを制限しています。  
- [Windows Server 2012 R2 のクライアントアクセスポリシー AD FS](Access-Control-Policies-W2K12.md)
- [AD FS 2.0 のクライアントアクセスポリシー](Access-Control-Policies-in-AD-FS-2.md)

これらのポリシーの例を次に示します。
- Office 365 へのすべてのエクストラネットクライアントアクセスをブロックする
- Exchange Active Sync の Exchange Online にアクセスするデバイスを除く、すべてのエクストラネットクライアントの Office 365 へのアクセスをブロックする

多くの場合、これらのポリシーの背後での基盤となるニーズは、承認されたクライアント、データをキャッシュしないアプリケーション、またはリモートから無効化できるデバイスがリソースにアクセスできることを保証することで、データ漏えいのリスクを軽減することです。

前述した特定のシナリオでの AD FS 作業に関するポリシーはドキュメントに記載されていますが、常に使用できるとは限らないクライアントデータに依存しているため、制限があります。  たとえば、クライアントアプリケーションの id は、SharePoint Online などのリソースではなく、Exchange Online ベースのサービスでのみ使用でき、ブラウザーまたは Word や Excel などの "シッククライアント" を介して同じデータにアクセスする可能性があります。  また AD FS SharePoint Online や Exchange Online など、Office 365 内のリソースがアクセスされていないことを認識しています。

これらの制限に対処し、ポリシーを使用して Office 365 またはその他の Azure AD ベースのリソースのビジネスデータへのアクセスを管理するためのより堅牢な方法を提供するために、Microsoft は Azure AD 条件付きアクセスを導入しました。  Azure AD 条件付きアクセスポリシーは、特定のリソース、または Azure AD の Office 365、SaaS、またはカスタムアプリケーション内の任意のリソースまたはすべてのリソースに対して構成できます。  これらのポリシーは、デバイスの信頼、場所、およびその他の要因をピボットします。

Azure AD 条件付きアクセスの詳細については、「 [」の「条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)」を参照してください Azure Active Directory

これらのシナリオを実現するための重要な変更は[先進認証](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)で、Office クライアント、Skype、Outlook、およびブラウザーで同じように動作するユーザーとデバイスを認証する新しい方法です。

## <a name="next-steps"></a>次の手順
クラウドとオンプレミスの間でアクセスを制御する方法の詳細については、以下を参照してください。

- [Azure Active Directory での条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
- [AD FS 2016 の Access Control ポリシー](Access-Control-Policies-in-AD-FS.md)
