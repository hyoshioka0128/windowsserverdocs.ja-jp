---
title: "ソフトウェアの制限のポリシーをメール ウイルスからコンピューターを保護するために使用します。"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 41b4c2399a86ef96d34b62295eda4a1ce9300609
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>ソフトウェアの制限のポリシーをメール ウイルスからコンピューターを保護するために使用します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、メール ウイルスから始まる Windows Server 2008 および Windows Vista からコンピューターを保護するために、ソフトウェア制限ポリシー (SRP) を使用してアプリケーション制御の設定方法のポリシー情報を提供します。

## <a name="introduction"></a>概要
ソフトウェア制限ポリシー (SRP) は、ドメイン内のコンピューターで実行されているソフトウェア プログラムを指定し、これらのプログラムを実行する機能を制御する、グループ ポリシー ベースの機能です。 厳しく制限されているしたアプリケーションに限って実行を許可する、コンピューターの構成を作成するのにには、ソフトウェアの制限のポリシーを使用します。 これらは、Microsoft Active Directory Domain Services とグループ ポリシーに統合されているが、スタンドアロン コンピューター上で構成することもあります。 SRP の開始点は、次を参照してください。、 [Software Restriction Policies](software-restriction-policies.md)します。

Windows Server 2008 R2 および Windows 7 以降、Windows AppLocker を使用できるの代わりに、または SRP と連動してアプリケーション制御戦略の一部を受け取ります。 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>電子メールのウイルスから保護するために SRP を構成します。

1.  ソフトウェアの制限のポリシーを SRP のしくみを理解するためのベスト プラクティスを確認します。

    -   [ベスト プラクティス](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [ソフトウェアの制限のポリシーのしくみ](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  ソフトウェアの制限のポリシーを開きます。

    -   [ローカル コンピューターに対して](administer-software-restriction-policies.md#BKMK_1)

    -   [ドメインのサイト、または組織単位、使用しているメンバー サーバーまたはドメインに参加しているワークステーション上](administer-software-restriction-policies.md#BKMK_2)

3.  ソフトウェアの制限のポリシーをまだ定義していない場合は、新しいソフトウェアの制限のポリシーを作成します。

    -   [新しいソフトウェアの制限のポリシーを作成するには](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  電子メール プログラムを使用して、電子メールの添付ファイルを実行するフォルダーのパスの規則を作成し、セキュリティ設定レベルを**許可しない**します。

    -   [パスの規則の操作](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  規則を適用するファイルの種類を指定します。

    -   [追加または指定されたファイルの種類を削除するには](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  ユーザーとグループを適用するために、ポリシー設定を変更します。

    -   ユーザーまたはグループをたくない、グループ ポリシー オブジェクト (GPO) を指定するポリシー設定を適用します。

    -   ローカル管理者を特定のポリシー設定では、グループ ポリシーのソフトウェアの制限のポリシーから除外して、他のグループ ポリシー管理者に適用します。

        -   [ソフトウェアの制限のポリシーをローカルの管理者に適用されないようにするには](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  ポリシーをテストします。


