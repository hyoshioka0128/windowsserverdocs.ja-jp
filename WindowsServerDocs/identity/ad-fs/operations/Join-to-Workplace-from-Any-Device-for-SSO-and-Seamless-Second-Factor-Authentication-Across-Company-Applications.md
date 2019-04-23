---
ms.assetid: e22d84a5-113d-4bec-b484-036ed29f0c28
title: 任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/05/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0ee22afd6fdec96ab69d915e4730bb834d2ab8ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855523"
---
# <a name="join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications"></a>任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証

>適用先:Windows Server 2012 R2

コンシューマー デバイスの数が急速に増加し、時間と場所を問わずに情報にアクセスできるようになった現在、人々のテクノロジに対する考え方も変化しています。 情報技術を一日中使用し続けるようになり、情報に簡単にアクセスできるようになったことで、従来の仕事とプライベートの区別はあいまいなものになっています。 信念を伴うこのようなテクノロジを選択し、ユーザーの個性、活動、およびスケジュールに合わせてカスタマイズされたその個人のワークプ レースに拡張する必要があります。 個人用のコンシューマー デバイスを企業ネットワークに接続したいという多数の要望に応えるため、Microsoft では次のような価値提供を行っています。

-   管理者は、社内リソースにアクセスできるユーザーをアプリケーション、ユーザー、デバイス、および場所に基づいて制御できます。

-   従業員は、任意のデバイスを使用してアプリケーションとデータにどこからでもアクセスできます。 さらに、ブラウザー アプリケーションや企業アプリケーションでシングル サインオンを使用できます。

## <a name="key-concepts-introduced-in-the-solution"></a>ソリューションに導入された重要な概念

### <a name="workplace-join"></a>社内参加
ワークプレース ジョインを使用すると、インフォメーション ワーカーは個人用のデバイスを職場のコンピューターに参加させて、社内のリソースやサービスにアクセスできます。 職場に参加した個人用のデバイスは既知のデバイスとなり、職場のリソースやアプリケーションに対するシームレスな 2 要素認証とシングル サインオンが可能になります。 ワークプレース ジョインによってデバイスを職場に参加させると、そのデバイスの属性をディレクトリから取得して、アプリケーションに対するセキュリティ トークンの発行を承認するために条件付きアクセスを実行できます。 Windows 8.1 と iOS 6.0 以上、および Android 4.0 以上のデバイスでは、ワークプレース ジョインを使用して Windows 8.1 および iOS デバイスを参加させることができます。

### <a name="BKMK_DRS"></a>Azure Active Directory Device Registration サービス
ワークプレース ジョインは、Azure Active Directory Device Registration サービスによって可能になります。 デバイスをワークプレース ジョインによって参加させると、このサービス は Azure Active Directory にデバイス オブジェクトをプロビジョニングし、デバイス ID を表すために使用されるキーをローカル デバイスに設定します。 このデバイス ID は、クラウドとオンプレミスでホストされているアプリケーションのアクセス制御規則と共に使用できます。

詳細については、次を参照してください。 [Azure Active Directory でデバイス管理の概要](https://docs.microsoft.com/azure/active-directory/device-management-introduction)します。

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

1.  [チュートリアル: Windows デバイスのワークプ レース ジョイン](../../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)

2.  [チュートリアル: IOS デバイスのワークプ レース ジョイン](../../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

3.  [チュートリアル: Android デバイスでワークプ レース ジョイン](../../ad-fs/operations/walkthrough--workplace-join-to-an-android-device.md)

## <a name="see-also"></a>関連項目
[デバイス登録サービスによるフェデレーション サーバーを構成します。](../deployment/configure-a-federation-server-with-device-registration-service.md)



