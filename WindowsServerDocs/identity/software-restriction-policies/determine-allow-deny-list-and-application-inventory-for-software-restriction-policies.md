---
title: "ソフトウェアの制限のポリシーの許可/拒否リストとアプリケーション インベントリを決定します。"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 60e78912284715649938567d66ffb90b9890b1b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>ソフトウェアの制限のポリシーの許可/拒否リストとアプリケーション インベントリを決定します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

IT プロフェッショナル向けのこのトピックでは、許可を作成し、ソフトウェア制限ポリシー (SRP) 以降は、Windows Server 2008 および Windows Vista でによって管理されるアプリケーションの一覧を拒否する方法ガイダンスを提供します。

## <a name="introduction"></a>概要
ソフトウェア制限ポリシー (SRP) は、ドメイン内のコンピューターで実行されているソフトウェア プログラムを指定し、これらのプログラムを実行する機能を制御する、グループ ポリシー ベースの機能です。 厳しく制限されているしたアプリケーションに限って実行を許可する、コンピューターの構成を作成するのにには、ソフトウェアの制限のポリシーを使用します。 これらは、Microsoft Active Directory Domain Services とグループ ポリシーに統合されているが、スタンドアロン コンピューター上で構成することもあります。 SRP の開始点は、次を参照してください。、 [Software Restriction Policies](software-restriction-policies.md)します。

Windows Server 2008 R2 および Windows 7 以降、Windows AppLocker を使用できるの代わりに、または SRP と連動してアプリケーション制御戦略の一部を受け取ります。

SRP を使用して特定のタスクを実行する方法については、次を参照してください。

-   [ソフトウェアの制限のポリシー規則を使用します。](work-with-software-restriction-policies-rules.md)

-   [ソフトウェアの制限のポリシーをメール ウイルスからコンピューターを保護するために使用します。](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>どのような既定の規則を選択する: 許可または拒否
既定の規則のベースである 2 つのモードのいずれかでソフトウェアの制限のポリシーを展開することができます。許可リストまたは拒否リスト。 お客様の環境で実行が許可されたすべてのアプリケーションを識別するポリシーを作成することができます。既定の規則、ポリシー内では、制限されたは実行を明示的に許可しないすべてのアプリケーションをブロックします。 またはを実行できません。すべてのアプリケーションを識別するポリシーを作成することができます。既定の規則は、[制限なし]、明示的に表示されているアプリケーションのみを制限します。

> [!IMPORTANT]
> 拒否リスト モードには、アプリケーション制御に関する組織の高メンテナンス戦略可能性があります。 作成して、すべてのマルウェアやその他の問題があるアプリケーションを禁止するにおいて変化し続けるリストを保持するでしょう時間がかかる犯しやすい間違いを受けやすくなります。

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>許可リストに、アプリケーションのインベントリを作成します。
許可する既定の規則を効果的に使用するには、組織でどのアプリケーションが必要な正確に決定する必要があります。 Microsoft Application Compatibility Toolkit のインベントリ コレクターなど、アプリケーション インベントリを作成するように設計するツールがあります。 SRP が正確にどのようなアプリケーションを実行している環境内を理解するのに役立つ、詳細ログ機能。

##### <a name="to-discover-which-applications-to-allow"></a>許可するようにアプリケーションを検出するには

1.  テスト環境では、[制限なし] に、既定の規則セットとソフトウェアの制限のポリシーを展開し、追加の規則を削除します。 強制的に任意のアプリケーションを制限することがなく SRP を有効にした場合、SPR はどのようなアプリケーションが実行されているかを監視できるようになります。

2.  詳細ログ機能を有効にして、ログ ファイルの書き込み先パスを設定するためには、次のレジストリ値を作成します。

    **"HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    文字列の値: *NameLogFile NameLogFile パス*

    ログ ファイルにエントリが書き込まれるため、SRP を実行するとき、すべてのアプリケーションを評価するが、*NameLogFile*たびにアプリケーションを実行します。

3.  ログ ファイルを評価します。

    各ログ エントリ記載されています。

    -   ソフトウェア制限ポリシーとプロセス ID (PID) の呼び出し元プロセスの最初の呼び出し

    -   評価されているターゲット

    -   そのアプリケーションが実行されたときに発生した、SRP の規則

    -   SRP の規則の識別子です。

    ログ ファイルに書き込まれる出力の例:

**explorer.exe (PID = 4728) 無制限 usingpath 規則、Guid として identifiedC:\Windows\system32\onenote.exe = {320bd852-aa7c-4674-82c5-9a80321670a3}**すべてのアプリケーションと SRP を確認し、ブロックする設定が関連付けられているコードを許可されている一覧をどの実行可能ファイルを考慮すべきかを判断し、使用できるログ ファイルに記録されます。


