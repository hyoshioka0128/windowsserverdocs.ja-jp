---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: 任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 82c94adadb9241e2b7cd8d75ea1693957aaffc61
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816265"
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証



コンシューマー デバイスの数が急速に増加し、時間と場所を問わずに情報にアクセスできるようになった現在、人々のテクノロジに対する考え方も変化しています。 情報技術を一日中使用し続けるようになり、情報に簡単にアクセスできるようになったことで、従来の仕事とプライベートの区別はあいまいなものになっています。 これらの変動は、個人のテクノロジを選択し、ユーザーの個性、活動、スケジュールに合わせてカスタマイズしたという確信を持っています。ワークプレースに拡張する必要があります。 個人用のコンシューマー デバイスを企業ネットワークに接続したいという多数の要望に応えるため、Microsoft では次のような価値提供を行っています。

-   管理者は、社内リソースにアクセスできるユーザーをアプリケーション、ユーザー、デバイス、および場所に基づいて制御できます。

-   従業員は、任意のデバイスを使用してアプリケーションとデータにどこからでもアクセスできます。 さらに、ブラウザー アプリケーションや企業アプリケーションでシングル サインオンを使用できます。

## <a name="key-concepts-introduced-in-the-solution"></a>ソリューションに導入された重要な概念

### <a name="workplace-join"></a>社内参加
ワークプレース ジョインを使用すると、インフォメーション ワーカーは個人用のデバイスを職場のコンピューターに参加させて、社内のリソースやサービスにアクセスできます。 職場に参加した個人用のデバイスは既知のデバイスとなり、職場のリソースやアプリケーションに対するシームレスな 2 要素認証とシングル サインオンが可能になります。 ワークプレース ジョインによってデバイスを職場に参加させると、そのデバイスの属性をディレクトリから取得して、アプリケーションに対するセキュリティ トークンの発行を承認するために条件付きアクセスを実行できます。 Windows 8.1 と iOS 6.0 以上、および Android 4.0 以上のデバイスでは、ワークプレース ジョインを使用して Windows 8.1 および iOS デバイスを参加させることができます。

### <a name="azure-active-directory-device-registration-service"></a><a name="BKMK_DRS"></a>Azure Active Directory Device Registration サービス
ワークプレース ジョインは、Azure Active Directory Device Registration サービスによって可能になります。 デバイスをワークプレース ジョインによって参加させると、このサービス は Azure Active Directory にデバイス オブジェクトをプロビジョニングし、デバイス ID を表すために使用されるキーをローカル デバイスに設定します。 このデバイス ID は、クラウドとオンプレミスでホストされているアプリケーションのアクセス制御規則と共に使用できます。

詳細については、「 [Azure Active Directory でのデバイス管理の概要](https://docs.microsoft.com/azure/active-directory/device-management-introduction)」を参照してください。

### <a name="workplace-join-as-a-seamless-second-factor-authentication"></a>シームレスな 2 要素認証としてのワークプレース ジョイン
会社は、コンシューマー デバイスに社内リソースへのアクセスを許可しつつ、情報へのアクセスに関連するリスクを管理して、ガバナンスとコンプライアンスを実施することができます。 デバイスのワークプレース ジョインでは、管理者は次の操作を実行できます。

-   デバイス認証を使用して既知のデバイスを識別します。 管理者はこの情報を使用して、条件付きアクセスを実行し、リソースへのアクセスを制御します。

-   信頼されたデバイスから社内リソースにアクセスするユーザーに、よりシームレスなサインイン エクスペリエンスを提供します。

### <a name="single-sign-on"></a>シングル サインオン
このシナリオで使用されるシングル サインオン (SSO) は、既知のデバイスから社内リソースにアクセスするためにエンド ユーザーが入力する必要があるパスワード プロンプトの表示回数を減らす機能です。 この機能により、SSO の有効期間内であれば、ユーザーはパスワードを 1 回入力するだけで、既知のデバイスから会社のアプリケーションやリソースにアクセスできます。 デバイスでワークプレース ジョインを使用する場合、このデバイスを使用するよう登録されたユーザーの SSO は既定で 7 日間、有効になります。 このユーザーには、同一セッションまたは新しいセッションでシームレスなサインイン エクスペリエンスが提供されます。

## <a name="solution-overview"></a>ソリューションの概要
このソリューションの一部として、サポートされているデバイスでワークプレース ジョインを使用して、社内リソースへのシングル サインオンを有効にする方法を学習します。

> [!NOTE]
> Windows 8.1、iOS 6.0 以降、および Android 4.0 以降のデバイスをサポートするには、Azure Active Directory Device Registration をデバイス オブジェクトの書き戻しと一緒に構成する必要があります (「 [Azure Active Directory Device Registration を使用してオンプレミスの条件付きアクセスを設定する](https://msdn.microsoft.com/library/azure/dn788908.aspx)」を参照してください)

このソリューション ガイドでは、次のチュートリアル手順が用意されています。

1.  [チュートリアル: Windows デバイスでの Workplace Join](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [チュートリアル: iOS デバイスでの Workplace Join](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [チュートリアル: Android デバイスでの Workplace Join](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>参照
[デバイス登録サービスを使用してフェデレーションサーバーを構成する](../deployment/configure-a-federation-server-with-device-registration-service.md)



