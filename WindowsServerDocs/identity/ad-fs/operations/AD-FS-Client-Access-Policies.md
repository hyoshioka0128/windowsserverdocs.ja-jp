---
ms.assetid: 
title: "AD FS のクライアント アクセス制御ポリシー"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5e1e1b907e6fccbf2b9906106d3360bd9a6fd69d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="controlling-access-to-organizational-data-with-active-directory-federation-services"></a>Active Directory フェデレーション サービスで組織のデータにアクセスを制御します。

このドキュメントでは、オンプレミスで AD FS を使用したアクセス制御の概要とのハイブリッド クラウド シナリオです。  

## <a name="ad-fs-and-conditional-access-to-on-premises-resources"></a>AD FS と内部設置型のリソース上に条件付きアクセス 
Active Directory フェデレーション サービスの概要については、以降は、承認ポリシーを制限またはユーザー要求の属性に基づいたリソースおよびリソースへのアクセスを許可する使用可能なされています。  AD FS は、バージョンごとに移動されたが、これらのポリシーの実装方法が変更されました。  バージョンでアクセス制御機能の詳細については、次を参照してください。
- [Windows Server 2016 の AD FS のアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)
- [Windows Server 2012 R2 の AD FS でのアクセス制御](Manage-Risk-with-Conditional-Access-Control.md)


## <a name="ad-fs-and-conditional-access-in-a-hybrid-organization"></a>AD FS とハイブリッド組織内の条件付きアクセス  

AD FS では、ハイブリッド シナリオでは条件付きアクセス ポリシーの上の内部設置型コンポーネントを提供します。 AD FS ベースの承認規則に対して使用するか、非 Azure AD のリソースのように内部設置型アプリケーションが AD FS に直接統合します。  クラウドのコンポーネントがによって提供される[Azure AD の条件付きアクセス](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)します。  Azure AD Connect は、2 つの接続のコントロール平面を提供します。

たとえば、クラウド リソースへの条件付きアクセス用の Azure AD にデバイスを登録するとき、Azure AD Connect デバイスの書き戻しを使用して適用するポリシーを AD FS のオンプレミス機能が利用可能なにあるデバイスの登録情報を使用します。  これにより、両方の内部設置型のアクセス制御ポリシーと、クラウド リソースを一貫した方法があります。  

![条件付きアクセス](../deployment/media/Plan-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  


### <a name="the-evolution-of-client-access-policies-for-office-365"></a>Office 365 のアクセス ポリシーをクライアントの展開
多くのユーザーを使用しているクライアントのアクセス ポリシーを AD FS と共にを Office 365 と、クライアントと使用されているクライアント アプリケーションの種類の場所などの要因に基づいて他の Microsoft Online services へのアクセスを制限します。  
- [Windows Server 2012 R2 AD FS のクライアント アクセス ポリシー](Access-Control-Policies-W2K12.md)
- [AD FS 2.0 でアクセス ポリシーをクライアント](Access-Control-Policies-in-AD-FS-2.md)

これらのポリシーの例をいくつか次のとおりです。
- Office 365 へのすべてのクライアントのエクストラネット アクセスをブロックします。
- Exchange Active Sync の Exchange Online にアクセスするデバイスを除く、Office 365 へのすべてのエクストラネット クライアント アクセスをブロックします。

多くの場合、基になる必要があるこれらのポリシーの内側に承認されたクライアントのみ、データをキャッシュしないアプリケーションのことを確認して、データ漏洩のリスクを軽減するか、またはデバイスをリモートで無効にするには、リソースへのアクセスを取得できます。

上記の文書化されたポリシーの AD FS の文書化されている特定のシナリオで機能しますが、必要である制限が一貫して使用できないクライアントのデータに依存するためです。  たとえば、クライアント アプリケーションの ID は、Exchange Online ベースのサービスと SharePoint Online、ブラウザーまたは Word や Excel などのシック (thick) クライアントを使用して、同じデータをアクセス可能性があるなどのリソースのではなく使用のみされています。  AD FS では、Office 365 SharePoint Online、Exchange Online など、アクセス対象のリソースの認識しません。

Office 365 またはその他の Azure AD ベースのリソースのビジネス データにアクセスを管理するポリシーをこれらの制限事項に対処し、使用するより堅牢な方法を提供する、Microsoft が Azure AD の条件付きアクセスを導入します。  Azure AD の条件付きアクセス ポリシーは、Azure ad または Office 365、SaaS またはカスタム アプリケーション内の一部またはすべてのリソースの特定のリソースを構成できます。  これらのポリシーは、デバイスの信頼、場所、およびその他の要因に注目します。

Azure AD の条件付きアクセスの詳細を参照してください[Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)

これらのシナリオを有効にすると、キーの変更は[最新の認証](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)、Office クライアント、Skype、Outlook、およびブラウザー全体で同じように動作しているユーザーとデバイスを認証するための新しい方法です。

## <a name="next-steps"></a>次の手順
詳細についてはオンプレミスとクラウド間のアクセスを制御するのには、次を参照してください。

- [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access)
- [AD FS 2016 でのアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)
