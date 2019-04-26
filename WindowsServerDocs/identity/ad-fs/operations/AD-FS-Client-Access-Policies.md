---
ms.assetid: ''
title: AD FS でクライアント アクセス制御ポリシー
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cc91cd9a446c8ca30471b65374ca99a7bd49d369
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882373"
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Active Directory フェデレーション サービスを組織のデータへのアクセスを制御します。

このドキュメントでは、AD FS を使用したアクセス制御の概要を示しますオンプレミス、ハイブリッドおよびクラウドのシナリオ。  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>AD FS とオンプレミスのリソースに対する条件付きアクセス 
Active Directory フェデレーション サービスの概要については、以降の承認ポリシーは制限またはユーザーの要求の属性に基づいたリソースとリソースへのアクセスを許可する使用可能なされています。  AD FS をバージョンごとに移動するときは、これらのポリシーを実装する方法が変更されました。  バージョンのアクセス制御機能の詳細については、次を参照してください。
- [Windows Server 2016 で AD FS でのアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)
- [Windows Server 2012 R2 で AD FS でのアクセス制御](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>AD FS とハイブリッド組織内の条件付きアクセス  

AD FS では、ハイブリッド シナリオでの条件付きアクセス ポリシーの上の内部設置型コンポーネントを提供します。 AD FS ベースの承認規則を付ける以外の Azure AD のリソースなど、オンプレミスのアプリケーションが AD FS に直接フェデレーションします。  クラウドのコンポーネントがによって提供される[Azure AD 条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)します。  Azure AD Connect では、2 つの接続の制御プレーンを提供します。

たとえば、クラウド リソースへの条件付きアクセス用に Azure AD でデバイスを登録するときに、Azure AD Connect デバイスの書き戻し機能を使用して適用するポリシーを AD FS のオンプレミス デバイスの登録情報を使用できます。  これにより、内部設置型の両方のアクセス制御ポリシーと、クラウド リソースを一貫した方法があります。  

![条件付きアクセス](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Office 365 のクライアント アクセス ポリシーの進化
AD FS を使用したクライアント アクセス ポリシーを使用して、Office 365 と、クライアントと使用されているクライアント アプリケーションの種類の場所などの要因に基づくその他の Microsoft Online services へのアクセスを制限する皆さんの多くは。  
- [Windows Server 2012 R2 AD FS でクライアント アクセス ポリシー](Access-Control-Policies-W2K12.md)
- [AD FS 2.0 でのクライアント アクセス ポリシー](Access-Control-Policies-in-AD-FS-2.md)

これらのポリシーのいくつかの例は次のとおりです。
- Office 365 へのすべてのエクストラネット クライアント アクセスをブロックします。
- デバイスが Exchange Active Sync の Exchange Online へのアクセスを除く、Office 365 へのすべてのエクストラネット クライアント アクセスをブロックします。

これらのポリシーの背後にある基になる必要が許可されたクライアントのみ、アプリケーションをデータをキャッシュしないようにすることでデータ漏えいのリスクを軽減するためには多くの場合、またはリモートで無効にできるデバイスは、リソースへのアクセスを取得できます。

AD FS の上記の文書化されているポリシーが記載されている特定のシナリオで動作が常に使用できるクライアントのデータに依存しているため、制限事項があります。  たとえば、クライアント アプリケーションの id のみがベースの Exchange Online サービスと SharePoint Online、ブラウザーまたは Word や Excel などのシック クライアントを使用して、同じデータをアクセス可能性があるなどのリソースではなくに使用できます。  また AD FS では、SharePoint Online または Exchange Online など、アクセスされている Office 365 内のリソースの認識しません。

これらの制限を解消し、使用するより堅牢な方法を提供する Office 365 またはその他の Azure AD ベースのリソースでのビジネス データへのアクセスを管理するポリシーは、Microsoft が Azure AD 条件付きアクセスを導入しました。  Azure AD 条件付きアクセス ポリシーは、Azure ad または Office 365、SaaS またはカスタム アプリケーション内のいずれかまたはすべてのリソースに対して特定のリソースを構成できます。  これらのポリシーは、デバイスの信頼、場所、およびその他の要因にピボットします。

Azure AD 条件付きアクセスに関する詳細については、次を参照してください[Azure Active Directory の条件付きアクセス。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)

これらのシナリオを有効にすると、キーの変更は[先進認証](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)、Office クライアント、Skype、Outlook、およびブラウザーの間で同じように機能を認証するためのユーザーとデバイスの新しい方法です。

## <a name="next-steps"></a>次の手順
オンプレミスとクラウド間でのアクセスを制御する詳細については、次を参照してください。

- [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access)
- [AD FS 2016 でのアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)
