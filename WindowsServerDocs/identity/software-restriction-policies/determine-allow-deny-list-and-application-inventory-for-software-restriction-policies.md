---
title: ソフトウェアの制限のポリシーの許可/拒否リストおよびアプリケーション インベントリの決定
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 0abb73b6-b5d8-4505-8ab1-2f29e4bf0411
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 7609ebb0fdcb6d429cd40d99399eaaedb732df08
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855095"
---
# <a name="determine-allow-deny-list-and-application-inventory-for-software-restriction-policies"></a>ソフトウェアの制限のポリシーの許可/拒否リストおよびアプリケーション インベントリの決定

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

IT プロフェッショナル向けのこのトピックでは、Windows Server 2008 および Windows Vista 以降のソフトウェア制限ポリシー (SRP) によって管理されるアプリケーションの許可リストと拒否リストを作成する方法について説明します。

## <a name="introduction"></a>はじめに
ソフトウェアの制限のポリシー (SRP) はグループ ポリシー ベースの機能で、ドメイン内のコンピューターで実行されているソフトウェア プログラムを識別し、これらのプログラムを実行する機能を制御します。 ソフトウェアの制限のポリシーを使えば、コンピューターの構成に厳格な制限を加え、指定したアプリケーションに限って実行を許可することができます。 これらは Microsoft Active Directory Domain Services およびグループポリシーと統合されていますが、スタンドアロンコンピューターで構成することもできます。 SRP の開始点については、「[ソフトウェアの制限のポリシー](software-restriction-policies.md)」を参照してください。

Windows Server 2008 R2 および Windows 7 以降では、アプリケーション制御戦略の一部として、または SRP と連携して Windows AppLocker を使用できます。

SRP を使用して特定のタスクを実行する方法については、以下を参照してください。

-   [ソフトウェア制限ポリシーの規則の使用](work-with-software-restriction-policies-rules.md)

-   [ソフトウェアの制限のポリシーを使用して、電子メールのウイルスからコンピューターを保護する](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

### <a name="what-default-rule-to-choose-allow-or-deny"></a>選択する既定の規則: 許可または拒否
ソフトウェアの制限のポリシーは、既定の規則 (許可リストまたは拒否リスト) の基礎となる2つのモードのいずれかで展開できます。 環境内で実行が許可されているすべてのアプリケーションを識別するポリシーを作成できます。ポリシー内の既定の規則は制限されており、明示的に実行を許可していないすべてのアプリケーションはブロックされます。 または、実行できないすべてのアプリケーションを識別するポリシーを作成することもできます。既定の規則は無制限で、明示的に一覧表示されているアプリケーションのみを制限します。

> [!IMPORTANT]
> 拒否リストモードは、アプリケーションの制御に関して、組織にとって高いメンテナンス戦略である可能性があります。 すべてのマルウェアやその他の問題のあるアプリケーションを禁止する進化したリストを作成して維持することは、時間がかかり、誤りの影響を受ける可能性があります。

### <a name="create-an-inventory-of-your-applications-for-the-allow-list"></a>許可一覧のアプリケーションのインベントリを作成する
既定の許可規則を効果的に使用するには、組織で必要なアプリケーションを正確に特定する必要があります。 Microsoft Application Compatibility Toolkit のインベントリコレクターなど、アプリケーションインベントリを作成するためのツールが用意されています。 ただし、SRP には、環境内でどのアプリケーションが実行されているかを正確に把握するのに役立つ高度なログ記録機能があります。

##### <a name="to-discover-which-applications-to-allow"></a>許可するアプリケーションを検出するには

1.  テスト環境で、既定の規則を [無制限] に設定してソフトウェアの制限ポリシーを展開し、追加の規則をすべて削除します。 アプリケーションの制限を強制せずに SRP を有効にすると、SPR は実行されているアプリケーションを監視できるようになります。

2.  詳細ログ機能を有効にし、ログファイルを書き込む場所のパスを設定するために、次のレジストリ値を作成します。

    **"HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows\Safer\ CodeIdentifiers"**

    文字列値: namelogfile*への namelogfile パス*

    SRP では実行時にすべてのアプリケーションが評価されるため、アプリケーションが実行されるたびに、エントリがログファイルの*Namelogfile*に書き込まれます。

3.  ログファイルを評価する

    各ログエントリの状態は次のとおりです。

    -   ソフトウェアの制限のポリシーの呼び出し元と、呼び出し元のプロセスのプロセス ID (PID)

    -   評価されるターゲット

    -   アプリケーションの実行時に発生した SRP 規則

    -   SRP 規則の識別子。

    ログファイルに書き込まれる出力の例を次に示します。

explorer.exe **(PID = 4728) identifiedC:\ Windows\system32\onenote.exe As 無制限の実行パスの規則、Guid = {320bd852-aa7c-4674-82c5-9a80321670a3}**   SRP によってチェックされブロックに設定されるすべてのアプリケーションと関連するコードは、ログファイルに記録されます。その後、許可リストについて考慮する必要がある実行可能ファイルを決定するために使用できます。


