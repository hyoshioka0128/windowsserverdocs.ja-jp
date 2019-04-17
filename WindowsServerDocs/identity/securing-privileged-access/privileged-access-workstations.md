---
title: "特権アクセス ワークステーション"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93589778-3907-4410-8ed5-e7b6db406513
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/09/2016
ms.openlocfilehash: ce64974d771a11ef11257bceef1c3fde1797a7da
ms.sourcegitcommit: 3bf47cf4e25896725137d983d63b8041a53cb9a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="privileged-access-workstations"></a>特権アクセス ワークステーション

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Privileged Access Workstations (PAWs) provide a dedicated operating system for sensitive tasks that is protected from Internet attacks and threat vectors. Separating these sensitive tasks and accounts from the daily use workstations and devices provides very strong protection from phishing attacks, application and OS vulnerabilities, various impersonation attacks, and credential theft attacks such as keystroke logging, [Pass-the-Hash](https://www.microsoft.com/en-us/download/details.aspx?id=36036), and [Pass-The-Ticket](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating%20Pass-the-Hash%20(PtH)%20Attacks%20and%20Other%20Credential%20Theft%20Techniques_English.pdf).

## <a name="architecture-overview"></a>Architecture Overview
The diagram below depicts a separate "channel" for administration (a highly sensitive task) that is created by maintaining separate dedicated administrative accounts and workstations.

![Diagram showing a separate "channel" for administration (a highly sensitive task) that is created by maintaining separate dedicated administrative accounts and workstations](../media/privileged-access-workstations/PAWFig1.JPG)

This architectural approach builds on the protections found in the Windows 10 [Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx) and [Device Guard](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx) features and goes beyond those protections for sensitive accounts and tasks.

This methodology is appropriate for accounts with access to high value assets:

-   **Administrative Privileges** the PAWs provide increased security for high impact IT administrative roles and tasks. This architecture can be applied to administration of many types of systems including Active Directory Domains and Forests, Microsoft Azure Active Directory tenants, Office 365 tenants, Process Control Networks (PCN), Supervisory Control and Data Acquisition (SCADA) systems, Automated Teller Machines (ATMs), and Point of Sale (PoS) devices.

-   **High Sensitivity Information workers** the approach used in a PAW can also provide protection for highly sensitive information worker tasks and personnel such as those involving pre-announcement Merger and Acquisition activity, pre-release financial reports, organizational social media presence, executive communications, unpatented trade secrets, sensitive research, or other proprietary or sensitive data. This guidance does not discuss the configuration of these information worker scenarios in depth or include this scenario in the technical instructions.

    > [!NOTE]
    > Microsoft IT uses PAWs (internally referred to as "secure admin workstations", or SAWs) to manage secure access to internal high-value systems within Microsoft. This guidance has additional details below on PAW usage at Microsoft in the section "How Microsoft uses admin workstations". For more detailed information on this high value asset environment approach, please refer to the article, [Protecting high-value assets with secure admin workstations](https://msdn.microsoft.com/en-us/library/mt186538.aspx).

This document will describe why this practice is recommended for protecting high impact privileged accounts, what these PAW solutions look like for protecting administrative privileges, and how to quickly deploy a PAW solution for domain and cloud services administration.

This document provides detailed guidance for implementing several PAW configurations and includes detailed implementation instructions to get you started on protecting common high impact accounts:

-   **Phase 1 - Immediate Deployment for Active Directory Administrators** this provides a PAW quickly that can protect on premises domain and forest administration roles

-   **Phase 2 - Extend PAW to all administrators** this enables protection for administrators of cloud services like Office 365 and Azure, enterprise servers, enterprise applications, and workstations

-   **Phase 3 - Advanced PAW security** this discusses additional protections and considerations for PAW security

### <a name="why-a-dedicated-workstation"></a>Why a dedicated workstation?
The current threat environment for organizations is rife with sophisticated phishing and other internet attacks that create continuous risk of security compromise for internet exposed accounts and workstations.

This threat environment requires an organizations to adopt an "assume breach" security posture when designing protections for high value assets like administrative accounts and sensitive business assets. These high value assets need to be protected against both direct internet threats as well as attacks mounted from other workstations, servers, and devices in the environment.

![Figure showing the risk to managed assets if an attacker gains control of a user workstation where sensitive credentials are used](../media/privileged-access-workstations/PAWFig2.JPG)

This figure depicts risk to managed assets if an attacker gains control of a user workstation where sensitive credentials are used.

An attacker in control of an operating system has numerous ways in which to illicitly gain access to all activity on the workstation and impersonate the legitimate account. A variety of known and unknown attack techniques can be used to gain this level of access. The increasing volume and sophistication of cyberattacks have made it necessary to extend that separation concept to completely separate client operating systems for sensitive accounts. For more information on these types of attacks, please visit the [Pass The Hash web site](https://www.microsoft.com/pth) for informative white papers, videos and more.

The PAW approach is an extension of the well-established recommended practice to use separate admin and user accounts for administrative personnel. This practice uses an individually assigned administrative account that is completely separate from the user's standard user account. PAW builds on that account separation practice by providing a trustworthy workstation for those sensitive accounts.

> [!NOTE]
> Microsoft IT uses PAWs (internally referred to as "secure admin workstations", or SAWs) to manage secure access to internal high-value systems within Microsoft.  This guidance has additional details on PAW usage at Microsoft in the section "How Microsoft uses admin workstations"
>
> For more detailed information on this high value asset environment approach, please refer to the article [Protecting high-value assets with secure admin workstations](https://msdn.microsoft.com/en-us/library/mt186538.aspx).

This PAW guidance is intended to help you implement this capability for protecting high value accounts such as high-privileged IT administrators and high sensitivity business accounts. The guidance helps you:

-   Restrict exposure of credentials to only trusted hosts

-   Provide a high-security workstation to administrators so they can easily perform administrative tasks.

Restricting the sensitive accounts to using only hardened PAWs is a straightforward protection for these accounts that is both highly usable for administrators and very difficult for an adversary to defeat.

#### <a name="alternate-approaches---limitations-considerations-and-integration"></a>Alternate approaches - Limitations, considerations, and integration
This section contains information on how the security of alternate approaches compares to PAW and how to correctly integrate these approaches within a PAW architecture. All of these approaches carry significant risks when implemented in isolation, but can add value to a PAW implementation in some scenarios.

**Credential Guard and Microsoft Passport**

Introduced in Windows 10, [Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx) uses hardware and virtualization-based security to mitigate common credential theft attacks, such as Pass-the-Hash, by protecting the derived credentials. The private key for credentials used by [Microsoft Passport](http://aka.ms/passport) can be also be protected by Trusted Platform Module (TPM) hardware.

These are powerful mitigations, but workstations can still be vulnerable to certain attacks even if the credentials are protected by Credential Guard or Passport. Attacks can include abusing privileges and use of credentials directly from a compromised device, reusing previously stolen credentials prior to enabling Credential Guard, and abuse of management tools and weak application configurations on the workstation.

The PAW guidance in this section includes the use of many of these technologies for high sensitivity accounts and tasks.

**Administrative VM**

An administrative virtual machine (VM) is a dedicated operating system for administrative tasks hosted on a standard user desktop. While this approach is similar to PAW in providing a dedicated OS for administrative tasks, it has a fatal flaw in that the administrative VM is dependent on the standard user desktop for its security.

The diagram below depicts the ability of attackers to follow the control chain to the target object of interest with an Admin VM on a User Workstation and that it is difficult to create a path on the reverse configuration.

The PAW architecture does not allow for hosting an admin VM on a user workstation, but a user VM with a standard corporate image can be hosted on a PAW host to provide personnel with a single PC for all responsibilities.

![Diagram of the PAW architecture](../media/privileged-access-workstations/PAWFig9.JPG)

**Jump Server**

Administrative "Jump Server" architectures set up a small number administrative console servers and restrict personnel to using them for administrative tasks. This is typically based on remote desktop services, a 3rd-party presentation virtualization solution, or a Virtual Desktop Infrastructure (VDI) technology.

This approach is frequently proposed to mitigate risk to administration and does provide some security assurances, but the jump server approach by itself is vulnerable to certain attacks because it violates the ["clean source" principle](http://aka.ms/cleansource). クリーン ソースの原則には、同様に信頼できるセキュリティ保護されているオブジェクトとしてすべてのセキュリティの依存関係が必要です。

![Figure showing a simple control relationship](../media/privileged-access-workstations/PAWFig3.JPG)

This figure depicts a simple control relationship. オブジェクトを制御しているサブジェクトは、そのオブジェクトのセキュリティの依存関係です。 If an adversary can control a security dependency of a target object (subject), they can control that object.

The administrative session on the jump server relies on the integrity of the local computer accessing it. If this computer is a user workstation subject to phishing attacks and other internet-based attack vectors, then the administrative session is also subject to those risks.

![Figure showing how attackers can follow an established control chain to the target object of interest](../media/privileged-access-workstations/PAWFig4.JPG)

The figure above depicts how attackers can follow an established control chain to the target object of interest.

While some advanced security controls like multi-factor authentication can increase the difficulty of an attacker taking over this administrative session from the user workstation, no security feature can fully protect against technical attacks when an attacker has administrative access of the source computer (e.g. injecting illicit commands into a legitimate session, hijacking legitimate processes, and so on.)

The default configuration in this PAW guidance installs administrative tools on the PAW, but a jump server architecture can also be added if required.

![Figure showing how reversing the control relationship and accessing user apps from an admin workstation gives the attacker no path to the targeted object](../media/privileged-access-workstations/PAWFig5.JPG)

This figure shows how reversing the control relationship and accessing user apps from an admin workstation gives the attacker no path to the targeted object. The user jump server is still exposed to risk so appropriate protective controls, detective controls, and response processes should still be applied for that internet-facing computer.

This configuration requires administrators to follow operational practices closely to ensure that they don't accidentally enter administrator credentials into the user session on their desktop.

![Figure showing how accessing an administrative jump server from a PAW adds no path for the attacker into the administrative assets](../media/privileged-access-workstations/PAWFig6.JPG)

This figure shows how accessing an administrative jump server from a PAW adds no path for the attacker into the administrative assets. A jump server with a PAW allows in this case you to consolidate the number of locations for monitoring administrative activity and distributing administrative applications and tools. This adds some design complexity, but can simplify security monitoring and software updates if a large number of accounts and workstations are used in your PAW implementation. The jump server would need to be built and configured to similar security standards as the PAW.

**Privilege Management Solutions**

Privileged Management solutions are applications that provide temporary access to discrete privileges or privileged accounts on demand. Privilege management solutions are an extremely valuable component of a complete strategy to secure privileged access and provide critically important visibility and accountability of administrative activity.

These solutions typically use a flexible workflow to grant access and many have additional security features and capabilities like service account password management and integration with administrative jump servers. There are many solutions on the market that provide privilege management capabilities, one of which is Microsoft Identity Manager (MIM) privileged access management (PAM).

Microsoft recommends using a PAW to access privilege management solutions. Access to these solutions should be granted only to PAWs. Microsoft does not recommend using these solutions as a substitute for a PAW because accessing privileges using these solutions from a potentially compromised user desktop violates the [clean source](http://aka.ms/cleansource) principle as depicted in the diagram below:

![Diagram showing how Microsoft does not recommend using these solutions as a substitute for a PAW because accessing privileges using these solutions from a potentially compromised user desktop violates the clean source principle](../media/privileged-access-workstations/PAWFig7.JPG)

Providing a PAW to access these solutions enables you to gain the security benefits of both PAW and the privilege management solution, as depicted in this diagram:

![Diagram showing how providing a PAW to access these solutions enables you to gain the security benefits of both PAW and the privilege management solution](../media/privileged-access-workstations/PAWFig8.JPG)

> [!NOTE]
> These systems should be classified at the highest tier of the privilege they manage and be protected at or above that level of security. These are commonly configured to manage Tier 0 solutions and Tier 0 assets and should be classified at Tier 0.
> For more information on the tier model, see [http://aka.ms/tiermodel](http://aka.ms/tiermodel) For more information on Tier 0 groups, see Tier 0 equivalency in [Securing Privileged Access Reference Material](../securing-privileged-access/securing-privileged-access-reference-material.md).

For more information on deploying Microsoft Identity Manager (MIM) privileged access management (PAM), see [http://aka.ms/mimpamdeploy](http://aka.ms/mimpamdeploy)

#### <a name="how-microsoft-is-using-admin-workstations"></a>How Microsoft is using admin workstations
Microsoft uses the PAW architectural approach both internally on our systems as well as with our customers. Microsoft uses administrative workstations internally in a number of capacities including administration of Microsoft IT infrastructure, Microsoft cloud fabric infrastructure development and operations, and other high value assets.

This guidance is directly based on the Privileged Access Workstation (PAW) reference architecture deployed by our cybersecurity professional services teams to protect customers against cybersecurity attacks. The administrative workstations are also a key element of the strongest protection for domain administration tasks, the Enhanced Security Administrative Environment (ESAE) administrative forest reference architecture.

For more details on the ESAE administrative forest, see [ESAE Administrative Forest Design Approach](http://aka.ms/ESAE) section in [Securing Privileged Access Reference Material](../securing-privileged-access/securing-privileged-access-reference-material.md).

For more information on engaging Microsoft services to deploy a PAW or ESAE for your environment, contact your Microsoft representative or visit [this page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

### <a name="what-is-a-privileged-access-workstation-paw"></a>What is a Privileged Access Workstation (PAW)?
In simplest terms, a PAW is a hardened and locked down workstation designed to provide high security assurances for sensitive accounts and tasks.  PAWs are recommended for administration of identity systems, cloud services, and private cloud fabric as well as sensitive business functions.

> [!NOTE]
> The PAW architecture doesn't require a 1:1 mapping of accounts to workstations, though this is a common configuration. PAW creates a trusted workstation environment that can be used by one or more accounts.

In order to provide the greatest security, PAWs should always run the most up-to-date and secure operating system available: Microsoft strongly recommends Windows 10 Enterprise, which includes a number of additional security features not available in other editions (in particular, [Credential Guard](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx) and [Device Guard](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx)).

> [!NOTE]
> Organizations without access to Windows 10 Enterprise can use Windows 10 Pro, which includes many of the critical foundational technologies for PAWs, including Trusted Boot, BitLocker, and Remote Desktop.  Education customers can use Windows 10 Education.  Windows 10 Home should not be used for a PAW.
>
> For a comparison matrix of the different editions of Windows 10, read [this article](https://www.microsoft.com/en-us/WindowsForBusiness/Compare).

The security controls in PAW are focused on mitigating the highest impact and most likely risks of compromise. These include mitigating attacks on the environment and mitigating risks that the PAW controls may degrade over time:

-   **Internet attacks** - Most attacks originate directly or indirectly from internet sources and use the internet for exfiltration and command and control (C2). Isolating the PAW from the open internet is a key element to ensuring the PAW is not compromised.

-   **Usability risk** - If a PAW is too difficult to use for daily tasks, administrators will be motivated to create workarounds to make their jobs easier. Frequently, these workarounds open the administrative workstation and accounts to significant security risks, so it's critical to involve and empower the PAW users to mitigate these usability issues securely. This is frequently accomplished by listening to their feedback, installing tools and scripts required to perform their jobs, and ensuring all administrative personnel are aware of why they need to use a PAW, what a PAW is, and how to use it correctly and successfully.

-   **Environment risks** - Because many other computers and accounts in the environment are exposed to internet risk directory or indirectly, a PAW must be protected against attacks from compromised assets in the production environment. This requires limiting the management tools and accounts that have access to the PAWs to the absolute minimum required to secure and monitor these specialized workstations.

-   **Supply chain tampering** - While it's impossible to remove all possible risks of tampering in the supply chain for hardware and software, taking a few key actions can mitigate critical attack vectors that are readily available to attackers. This includes validating the integrity of all installation media ([Clean Source Principle](http://aka.ms/cleansource)) and using a trusted and reputable supplier for hardware and software.

-   **Physical attacks** - Because PAWs can be physically mobile and used outside of physically secure facilities, they must be protected against attacks that leverage unauthorized physical access to the computer.

> [!NOTE]
> A PAW will not protect an environment from an adversary that has already gained administrative access over an Active Directory Forest.
> Because many existing implementations of Active Directory Domain Services have been operating for years at risk of credential theft, organizations should assume breach and consider the possibility that they may have an undetected compromise of domain or enterprise administrator credentials. ドメインのセキュリティ侵害が疑われる組織は、プロフェッショナルなインシデント レスポンス サービスの使用を検討する必要があります。
>
> 対応と回復のガイダンスについて詳しくは、「不審なアクティビティに対応」を参照してください。とのセクションでは"侵害から Recover" [Mitigating-Pass-the-hash およびその他の資格情報の盗難](https://www.microsoft.com/pth)、バージョン 2 です。
>
> 参照してください[マイクロソフトのインシデント レスポンスおよびリカバリ サービス](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)詳細については、ページ。

### <a name="paw-hardware-profiles"></a>PAW ハードウェア プロファイル
管理者は標準ユーザーが多すぎる - だけでなく、PAW が標準ユーザー ワークステーション電子メールをチェックし、Web の閲覧、企業の基幹業務アプリケーションにアクセスする必要があります。  管理者が生産性とセキュリティの両方を保持できることを確認することは、任意の PAW の展開の成功に不可欠です。  生産性を大幅に制限される安全なソリューションは (これは安全ではない方法で) 場合でも、生産性の向上を優先するユーザーから見向きもされなくなります。

ニーズと生産性向上のためのセキュリティのニーズのバランスを取るためには、マイクロソフトは、これらの PAW ハードウェア プロファイルのいずれかを使用してをお勧めします。

-   **専用のハードウェア**-個別のユーザー タスクと管理タスクの専用デバイス

-   **同時使用**-ユーザー タスクと管理タスク同時に実行できる OS またはプレゼンテーションの仮想化を利用して 1 つのデバイス。

組織には、1 つだけのプロファイルまたはその両方を使用可能性があります。 ハードウェア プロファイルとの間の相互運用性の問題がないと、組織がある、ハードウェア プロファイルを特定のニーズおよび特定の管理者の状況に合わせて柔軟にします。

> [!NOTE]
> 、でのこれらのシナリオすべてで、管理者が発行されるとは別の管理者アカウントが指定されている標準ユーザー アカウントが重要です。 管理者アカウントは、PAW 管理オペレーティング システムでのみ使用する必要があります。

次の表は、相対的な利点とやすさの運用と生産性、セキュリティの観点から各ハードウェア プロファイルの短所をまとめたものです。  両方のハードウェア アプローチでは、資格情報の盗難および再利用に対して管理アカウントの強力なセキュリティを提供します。

|**シナリオ**|**利点**|**短所**|
|--------|---------|-----------|
|専用のハードウェア|-機密タスク用の強力な信号<br />-最も強力なセキュリティの分離|-追加のデスク スペース<br />の (リモート作業) 用追加の重み付け<br />-ハードウェア コスト|
|同時使用|-ハードウェア コスト<br />-1 つのデバイス エクスペリエンス|不注意によるエラー/リスクのリスクを作成する 1 つのキーボード/マウスを共有|

このガイドには、専用のハードウェア アプローチの PAW 構成の詳細な手順が含まれています。 同時使用のハードウェア プロファイルの要件がある場合は、このガイドに基づく手順を採用するしたり、それを支援するマイクロソフトのような専門サービス組織を採用できます。

**専用のハードウェア**

このシナリオでは、電子メール、ドキュメントの編集、および開発作業などの日常の業務に使用する PC から完全に分離された管理のため、PAW が使用されます。 すべての管理ツールとアプリケーションが、PAW にインストールされているし、すべての生産性向上アプリケーションは、標準ユーザー ワークステーションにインストールされています。 このガイドの手順の説明については、このハードウェア プロファイルに基づいています。

**同時使用 - ローカル ユーザー VM を追加します。**

この同時使用シナリオでは、管理タスクと電子メール、ドキュメントの編集、および開発作業のような日常的な作業の両方の 1 台の PC が使用されます。 この構成では、ユーザーのオペレーティング システム (ドキュメントの編集やローカルにキャッシュされた電子メールで作業して)、切断中に利用可能ながこの切断状態に対応するハードウェアやサポート プロセスが必要です。

![電子メール、ドキュメントの編集、および開発作業などの管理タスクと日常的な作業の両方に使用する同時使用シナリオの 1 台の PC を示す図](../media/privileged-access-workstations/PAWFig10.JPG)

物理ハードウェアでは、2 つのオペレーティング システムがローカルで実行されます。

-   **管理 OS** -管理タスク用に PAW ホスト上に Windows 10 を実行する物理ホスト

-   **ユーザー OS** -企業のイメージを実行する Windows 10 クライアント Hyper-V 仮想マシンのゲスト

Windows 10Hyper-v、(Windows 10 を実行しているも)、ゲスト仮想マシンはサウンド、ビデオ、および Skype for Business などのインターネット通信のアプリケーションを含む充実したユーザー エクスペリエンスを持つことができます。

この構成では、会社用の正規の Windows 10 イメージが対象となりません、PAW ホストに適用される制限するユーザーの OS 仮想マシンで管理者特権を必要としない日常的な作業が行われます。 すべての管理作業は、管理 OS で行われます。

これを構成するには、の PAW ホストには、このガイドの指示に従って、クライアント Hyper-V 機能を追加するユーザー VM を作成し、ユーザー VM 上で Windows 10 の企業イメージをインストールします。

読み取り[クライアント Hyper-V](https://technet.microsoft.com/en-us/library/hh857623.aspx)」の記事の詳細については、この機能をします。 ゲスト仮想マシンでオペレーティング システム [あたりライセンスを取得する必要がありますに注意してください[マイクロソフト製品のライセンス](https://www.microsoft.com/en-us/Licensing/product-licensing/products.aspx)も説明されている、[ここ](https://www.microsoft.com/en-us/Licensing/learn-more/brief-windows-virtual-machine.aspx)します。

**同時使用 - RemoteApp、RDP、または、VDI の追加**

この同時使用シナリオでは、両方の管理タスクの 1 台の PC を使用し、日常的な電子メール、ドキュメントの編集、および開発と同様に動作します。 この構成では、ユーザーのオペレーティング システムの展開し、一元的に管理 (クラウド上またはデータ センター内) は切断されている間は使用できません。

![両方の管理タスクのために使用する同時使用シナリオの 1 台の PC を示す図と電子メール、ドキュメントの編集、および開発のような日常的な作業](../media/privileged-access-workstations/PAWFig11.JPG)

物理ハードウェアでは、ローカルで管理タスクの 1 つの PAW オペレーティング システムを実行して、Microsoft またはサード パーティ製リモート デスクトップ サービスの電子メール、ドキュメントの編集、および基幹業務アプリケーションなどのユーザーのアプリケーションに接続します。

この構成では、管理者特権を必要としない日常的な作業は、リモート os および PAW ホストに適用される制限の対象ではないアプリケーションで行われます。 すべての管理作業は、管理 OS で行われます。

これを構成するには、の PAW ホストには、このガイドの指示に従って、リモート デスクトップ サービスへのネットワーク接続を許可する、アプリケーションにアクセスを PAW ユーザーのデスクトップにショートカットを追加します。 リモート デスクトップ サービスは、多くの方法を含むでホストされる可能性があります。

-   既存のリモート デスクトップまたは VDI サービス (オンプレミスまたはクラウド)

-   内部設置型をインストールする新しいサービスまたはクラウド

-   構成済みの Office 365 テンプレートまたはインストール イメージを使用して azure RemoteApp

Azure RemoteApp の詳細については、次を参照してください。[このページ](https://www.remoteapp.windowsazure.com)します。

### <a name="paw-scenarios"></a>PAW のシナリオ
このセクションに適用するこの PAW ガイダンス シナリオに関するガイダンスが含まれています。 すべてのシナリオでのみリモート システムのサポートを実行するために Paw を使用する管理者をトレーニングする必要があります。 成功しており、セキュリティで保護された使用状況を促進するには、PAW のすべてのユーザーもされるすべき PAW エクスペリエンスを向上させるフィードバックと、このフィードバックは、PAW プログラムとの統合のために慎重に検討する必要がありますを提供します。

すべてのシナリオで、後の段階で追加のセキュリティを強化し、このガイドで別のハードウェア プロファイルがロールの利便性やセキュリティの要件を満たすために使用できます。

> [!NOTE]
> すべてのホスト、およびサービスに、このガイダンス明確に区別 (Azure や Office 365 管理ポータル) などのインターネットと「開かれたインターネット」で特定サービスへのアクセスを必要とする注意してください。

参照してください、[階層モデル ページ](http://aka.ms/tiermodel)階層指定の詳細についてはします。

|**シナリオ**|**PAW を使用しますか。**|**スコープおよびセキュリティの考慮事項**|
|---------|--------|---------------------|
|Active Directory 管理者 - 階層 0|うん|フェーズ 1 のガイダンスで構築された PAW は、このロールに対して十分です。<br /><br />-このシナリオで最も強力な保護を提供するのには、管理フォレストを追加することができます。 ESAE 管理フォレストの詳細については、次を参照してください[ESAE 管理フォレスト設計のアプローチ。](http://aka.ms/esae)<br />-PAW は、複数のドメインまたはフォレストが複数の管理に使用できます。<br />場合、ドメイン コントローラーは、Service (IaaS) またはオンプレミスの仮想化ソリューションとしてのインフラストラクチャでホストされているが、それらのソリューションの管理者用の Paw の実装を優先する必要があります。|
|管理者の Azure IaaS と PaaS サービス - 階層 0 または階層 1 (範囲と設計に関する考慮事項を参照してください)|うん|フェーズ 2 のガイダンスを使用して構築された PAW は、このロールに対して十分です。<br /><br />-Paw に使用するには、少なくともサブスクリプション課金管理者、全体管理者。 重要なまたは機密のサーバーの代理管理者の Paw を使用することも必要があります。<br />にオペレーティング システムを管理するため Paw を使用する必要があります、ディレクトリ同期および ID フェデレーションを提供するアプリケーションのクラウド サービスと[Azure AD Connect](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect/)と Active Directory Federation Services (ADFS)。<br />-外部ネットワーク制限では、フェーズ 2 のガイダンスを使用して、承認されたクラウド サービスにのみ接続を許可する必要があります。 Paw からオープンなインターネット アクセスを許可しないようにします。<br />-EMET は、ワークステーションで使用しているすべてのブラウザーを構成する必要があります**注:**サブスクリプションはする場合はドメイン コントローラーまたはその他の階層 0 ホストがサブスクリプション内、フォレストの階層 0 と見なされます。 階層 0 サーバーが Azure でホストされていない場合、サブスクリプションは階層 1 です。|
|管理者の Office 365 テナント <br />階層 1|うん|フェーズ 2 のガイダンスを使用して構築された PAW は、このロールに対して十分です。<br /><br />-Paw に使用するには、少なくともサブスクリプション課金管理者、全体管理者、Exchange 管理者、SharePoint 管理者、およびユーザー管理の管理者ロール。 強くも非常に重要なまたは機密のデータの代理管理者の Paw の使用を検討してください。<br />-EMET は、ワークステーションで使用しているすべてのブラウザーを構成する必要があります。<br />-外部ネットワーク制限では、フェーズ 2 のガイダンスを使用して Microsoft サービスにのみ接続を許可する必要があります。 Paw からオープンなインターネット アクセスを許可しないようにします。|
|その他の IaaS または PaaS クラウド サービスの管理<br />-階層 0 または階層 1 (範囲と設計に関する考慮事項を参照してください)||フェーズ 2 のガイダンスを使用して構築された PAW は、このロールに対して十分です。<br /><br />-ハード ドライブとオペレーティング システム、機密データ、またはビジネス クリティカルなデータが格納されているエージェントのインストール、ハード ディスク ファイルをエクスポートまたは記憶域にアクセスする機能を含むクラウドがホストされている Vm の管理者権限を持つすべてのロールに対して、Paw を使用する必要があります。<br />-外部ネットワーク制限では、フェーズ 2 のガイダンスを使用して Microsoft サービスにのみ接続を許可する必要があります。 Paw からオープンなインターネット アクセスを許可しないようにします。<br />-EMET は、すべてのブラウザーで、ワークステーションで使用される構成する必要があります。 **注:**サブスクリプションは、ドメイン コントローラーまたはその他の階層 0 ホストがサブスクリプション内にある場合、フォレストの階層 0 です。 階層 0 サーバーが Azure でホストされていない場合、サブスクリプションは階層 1 を使用します。|
|仮想化管理者<br />-階層 0 または階層 1 (範囲と設計に関する考慮事項を参照してください)|うん|フェーズ 2 のガイダンスを使用して構築された PAW は、このロールに対して十分です。<br /><br />-ハード ドライブとゲスト オペレーティング システムの情報、機密データ、またはビジネス クリティカルなデータが格納されているエージェントのインストール、仮想ハード ディスク ファイルをエクスポートまたは記憶域にアクセスする機能を含む Vm 経由で管理者権限を持つすべてのロールに対して、Paw を使用する必要があります。 **注:**仮想化システム (およびその管理者) と見なされます、フォレストの階層 0 のドメイン コントローラーまたはその他の階層 0 ホストがサブスクリプション内にある場合。 階層 0 サーバーが仮想化システムでホストされていない場合、サブスクリプションは階層 1 を使用します。|
|サーバー メンテナンス管理者<br />階層 1|うん|フェーズ 2 のガイダンスを使用して構築された PAW は、このロールに対して十分です。<br /><br />に管理者に、更新、パッチ適用、およびエンタープライズ サーバーと Windows server、Linux、およびその他のオペレーティング システムを実行しているアプリのトラブルシューティングを行うは、PAW を使用してください。<br />-専用の管理ツールは、これらの管理者の大きな規模で処理するために Paw に追加する必要があります。|
|ユーザー ワークステーション管理者 <br />階層 2|うん|フェーズ 2 のガイダンスを使用して構築された PAW は、管理者権限を持つエンド ユーザーのデバイスで (ヘルプデスクおよびデスクサイド サポートのロール) とロールに対して十分です。<br /><br />-その他のアプリケーションは、チケット管理やその他のサポート機能を有効にするために Paw にインストールする必要があります。<br />-EMET は、すべてのブラウザーで、ワークステーションで使用される構成する必要があります。<br />    専用の管理ツールは、これらの管理者の大きな規模で処理するために Paw に追加する必要があります。|
|SQL、SharePoint、または基幹業務 (LOB) 管理者<br />階層 1||フェーズ 2 のガイダンスで構築された PAW は、このロールに対して十分です。<br /><br />-追加の管理ツールは、リモート デスクトップを使用してサーバーに接続しなくてもアプリケーションを管理する管理者を許可するように Paw にインストールする必要があります。|
|ユーザーのソーシャル メディア サイトの管理|部分的に|フェーズ 2 のガイダンスを使用して構築された PAW は、これらのロールのセキュリティを提供する開始点として使用できます。<br /><br />保護し、Azure Active Directory (AAD) を使用して、共有、保護、およびソーシャル メディア アカウントへのアクセスを追跡のソーシャル メディア アカウントを管理します。<br />    この機能について詳しくは、読み取り[このブログ投稿](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)します。<br />-外部ネットワーク制限では、これらのサービスへの接続を許可する必要があります。 これは、オープンなインターネット接続 (はるかに高いセキュリティ リスク多くの paw を無効にする) を許可することで、または (が取得が困難な) サービスの必要な DNS アドレスのみを許可することで実行できます。|
|標準ユーザー|違います|標準ユーザーのセキュリティ強化に多くの手順を使用できますが、PAW はほとんどのユーザーが職務に必要とするオープンなインターネット アクセスからアカウントを分離するよう設計されています。|
|ゲスト VDI/キオスク|違います|ゲストのキオスク システムのセキュリティ強化に多くの手順を使用できますが、PAW アーキテクチャは、機密性の高いアカウント、機密性の低いアカウントのない高度なセキュリティを高度なセキュリティを提供するものです。|
|VIP ユーザー (Executive、研究者など)|部分的に|フェーズ 2 のガイダンスを使用して構築された PAW は、これらのロールのセキュリティを提供する開始点として使用できます。<br /><br />-このシナリオは標準ユーザーのデスクトップに似ていますが、通常より小さい、単純でよく知られたアプリケーション プロファイルには。 このシナリオは、通常、検出および機密性の高いデータ、サービス、および (場合がありますが、デスクトップ上にインストールされていない) アプリケーションを保護する必要があります。<br />-これらのロールは、通常、ユーザー設定に応じた設計の変更を必要とする高度なセキュリティと非常に高度な使いやすさが必要です。|
|工業用制御システム (例: SCADA、PCN、および DCS)|部分的に|フェーズ 2 のガイダンスを使用して構築された PAW を使用するオープンなインターネットの閲覧や電子メールのチェックほとんどの ICS、これらのロールのセキュリティを提供する開始点としてコンソール (SCADA および PCN などの共通標準を含む) が必要としません。<br /><br />-物理メカニズムを制御するために使用するアプリケーションは、統合しの互換性をテストし、適切に保護する必要|
|Embedded オペレーティング システム|違います|Embedded オペレーティング システムの PAW からセキュリティ強化に多くの手順を使用できますが、カスタム ソリューションは、このシナリオのセキュリティ強化を開発する必要があります。|

> [!NOTE]
> **組み合わせシナリオ**一部のユーザーが複数のシナリオにまたがる管理責任がある可能性があります。
> このような場合は、留意する重要な規則は、階層モデルのルールを常に従う必要があることです。 詳細については、階層モデル ページを参照してください。

> [!NOTE]
> **PAW プログラムをスケーリング**ように、PAW プログラムは、多くの管理者とロールが含まれるように拡張、引き続きセキュリティ標準規格と使いやすさの遵守を保持しておくことを確認する必要があります。 アドレスの使いやすさにフィードバックを収集の課題を構造をサポートまたは PAW オンボーディング プロセス、インシデント管理、構成管理] などの PAW 固有の課題を解決するのには、新たに作成する IT を更新して可能性があります。  1 つの例は、デスクトップ Paw からラップトップ Paw シフトでは追加のセキュリティに関する考慮事項が必要になる可能性がありますへのシフトが必要になると、管理者の在宅作業シナリオを有効にする、組織で決定する可能性があります。  別の一般的な例が作成または更新する必要があります、PAW の適切な使用上のコンテンツを含むようになりました新しい管理者向けのトレーニングが (理由を含むその重要性と新機能、PAW はありません)。  PAW プログラムを拡張するように対処する必要がありますが他の考慮事項」の手順のフェーズ 2 を参照してください。

このガイドには、上記のシナリオの PAW 構成の詳細な手順が含まれています。 その他のシナリオの要件がある場合は、このガイドに基づく手順を採用するしたり、それを支援するマイクロソフトのような専門サービス組織を採用できます。

環境に合わせてカスタマイズされた PAW を設計する Microsoft サービスの利用の詳細については、Microsoft の担当者に問い合わせるかを参照してください[このページ](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)します。

### <a name="paw-installation-instructions"></a>PAW のインストール手順
PAW は、管理用安全かつ信頼できるソースを提供しなければならないため、ビルド プロセスは、安全かつ信頼できることが重要です。  このセクションでは一般的な原則を使用して、独自の PAW を構築できる詳細な指示を提供し、マイクロソフト IT およびマイクロソフトによって使用されるものとよく似ています概念のクラウド エンジニア リングおよびサービス管理組織します。

指示がか所で最も重要な軽減策を迅速に配置徐々 に増加し、企業の PAW の使用を展開に重点を置いたの 3 つのフェーズに分かれています。

-   フェーズ 1 - Active Directory 管理者の迅速な展開

-   フェーズ 2 - すべての管理者への PAW の拡張

-   フェーズ 3 - 高度な PAW セキュリティ

ことが重要フェーズを常に実行することの順序でこれらの計画し、同じ全体的なプロジェクトの一部として実装されている場合でもに注意してください。

#### <a name="phase-1---immediate-deployment-for-active-directory-administrators"></a>フェーズ 1 - Active Directory 管理者の迅速な展開
目的: できる PAW を迅速、オンプレミス ドメインおよびフォレスト管理ロールを保護することができますを提供します。

範囲: 階層 0 の管理者は Enterprise Admins、Domain Admins (すべてのドメインの) およびその他の権限のある ID システムの管理者を含みます。

フェーズ 1 では、頻繁に攻撃の対象と非常に重要な役割は、内部設置型 Active Directory ドメインを管理する管理者に焦点を当てています。 これらの ID システムは、Azure infrastructure as a Service (IaaS) または他の IaaS プロバイダーの内部設置型のデータ センターで、Active Directory ドメイン コントローラー (Dc) がホストされているかどうかは、これらの管理者を保護するため効果的に動作します。

このフェーズでは、Paw 自体を展開できるだけでなく、特権アクセス ワークステーション (PAW) をホストにセキュリティで保護された管理 Active Directory 組織単位 (OU) 構造を作成します。  この構造体は、グループ ポリシーと PAW をサポートするために必要なグループにも含まれます。  提供されている PowerShell スクリプトを使用して構造体のほとんどは作成[TechNet ギャラリー](http://aka.ms/pawmedia)します。

スクリプトは、次の Ou とセキュリティ グループに作成されます。

-   組織単位 (OU)

    -   6 つの新しい最上位レベル Ou: Admin です。グループです。階層 1 のサーバーです。ワークステーションです。ユーザー アカウントです。コンピューターの検疫します。  各最上位レベル OU には、複数子 Ou にはが含まれます。

-   グループ

    -   6 つ新しいセキュリティ対応グローバル グループ: Tier 0 Replication Maintenance。階層 1 のサーバー メンテナンスです。Service Desk Operators です。ワークステーションのメンテナンスPAW ユーザーです。PAW Maintenance。

グループ ポリシー オブジェクトの数を作成します。PAW Configuration - コンピューターです。PAW Configuration - User;RestrictedAdmin Required - Computer です。PAW Outbound Restrictions です。ワークステーションのログオンを制限します。サーバーのログオンを制限します。

フェーズ 1 では、次の手順が含まれています。

1.  前提条件します。

    1.  **すべての管理者が管理およびエンド ユーザーのアクティビティを独立した個別のアカウントを使用することを確認**(電子メール、インターネットの閲覧、基幹業務アプリケーション、およびその他の管理者以外のアクティビティを含む)。  標準ユーザー アカウントから個々 の承認されているユーザーに管理者アカウントを割り当てることは、特定のアカウントのみが PAW 自体へのログオンを許可するように、PAW モデルの基盤です。

        > [!NOTE]
        > 各管理者は、自分のアカウントを使用して、管理する必要があります。  管理者アカウントを共有していません。

    2.  **階層 0 の特権を持つ管理者の数を最小限に抑える**します。  各管理者が PAW を使用する必要がありますので、管理者の数を減らすと、し、それに伴うコストをサポートするために必要な Paw の数が短縮されます。 これらの特権と関連するリスクの低い露出もで管理者の数が減少が増大します。 PAW を共有する 1 つの場所の管理者のことはできますが、個別の物理的な場所の管理者に別の Paw が必要です。

    3.  **すべての技術的な要件を満たしている信頼されたサプライヤーからハードウェアを入手**します。 Microsoft では、記事の技術的な要件を満たすハードウェアを入手ことをお勧め[Credential Guard によるドメインの資格情報の保護](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx)します。

        > [!NOTE]
        > これらの機能がないハードウェアにインストールされている PAW は、重要な保護を提供できますが、Credential Guard と Device Guard などの高度なセキュリティ機能は使用できません。  Credential Guard と Device Guard は、フェーズ 1 の展開に必要はありませんが、フェーズ 3 (高度なセキュリティ強化) の一部として強くお勧めします。

        PAW に使用するハードウェアをメーカーおよびサプライヤーするセキュリティ手順が組織によって信頼されてから提供されていることを確認します。 これは、サプライ チェーンのセキュリティにクリーン ソースの原則のアプリケーションです。

        > [!NOTE]
        > サプライ チェーンのセキュリティの重要性の詳細については、次を参照してください。[このサイト](https://www.microsoft.com/security/cybersecurity/)します。

    4.  入手して、必要な Windows 10 Enterprise Edition とアプリケーション ソフトウェアを検証します。 PAW に必要なソフトウェアを入手し、検証のガイダンスを使用して[クリーン ソース インストール メディアの](http://aka.ms/cleansource)します。

        -   Windows 10 Enterprise Edition

        -   [リモート サーバー管理ツール](https://www.microsoft.com/en-us/download/details.aspx?id=45520.)for Windows 10

        -   Windows 10[セキュリティ基本計画](http://aka.ms/win10baselines)

        -   [拡張 Mitigation Experience Toolkit (EMET)](https://www.microsoft.com/en-us/download/details.aspx?id=49166)

            > [!NOTE]
            > Microsoft は、すべてのオペレーティング システムと msdn の「アプリケーションに対して MD5 ハッシュ発行が、すべてのソフトウェア ベンダーが同様ドキュメントを提供します。  このような場合は、その他の戦略が必要になります。  ソフトウェアの検証の詳細についてを参照してください[クリーン ソース](http://aka.ms/cleansource)インストール メディアのします。

    5.  **イントラネット上の利用可能な WSUS サーバーがあることを確認**します。 ダウンロード、PAW の更新プログラムをインストールして、イントラネット上の WSUS サーバーを必要があります。 [この WSUS サーバーは、Windows 10 のすべてのセキュリティ更新プログラムを自動的に承認するように構成する必要があります。または管理の担当者が迅速にソフトウェアの更新プログラムの承認に適用する責任が必要です。

        > [!NOTE]
        > 詳細については、「"自動的に承認する更新プログラムのインストール」セクションを参照してください、[更新プログラムの承認](https://technet.microsoft.com/en-us/library/cc708458(v=ws.10).aspx)します。

2.  Paw をホストする管理 OU のフレームワークを展開します。

    1.  PAW スクリプト ライブラリからのダウンロード[TechNet ギャラリー](http://aka.ms/PAWmedia)

        > [!NOTE]
        > すべてのファイルをダウンロードし、同じディレクトリに保存下に示す順番で実行します。  Create-PAWGroups は Create-PAWOUs、によって作成された OU 構造に依存し、Set-PAWOUDelegation は Create-PAWGroups によって作成されるグループに依存します。
        > スクリプトまたはコンマ区切り値 (CSV) ファイルのいずれかを変更しないでください。

    2.  **Create-PAWOUs .ps1 スクリプトを実行して**します。  このスクリプトは、Active Directory で新しい組織単位 (OU) 構造を作成し、必要に応じて新しい Ou で GPO の継承をブロックします。

    3.  **Create-PAWGroups .ps1 スクリプトを実行して**します。  このスクリプトは、適切な Ou に、新しいグローバル セキュリティ グループが作成されます。

        > [!NOTE]
        > このスクリプトは新しいセキュリティ グループを作成、されませんが表示されますに自動的にします。

    4.  **Set-PAWOUDelegation .ps1 スクリプトを実行して**します。  このスクリプトでは、適切なグループに新しい Ou へのアクセス許可を割り当てます。

3.  **階層 0 のアカウントを admin \tier 0\Accounts OU に移動**します。 Domain Admin、Enterprise Admin のメンバーである各アカウントを移動または階層 0 の同等のグループ (入れ子になったメンバーシップを含む) をこの OU にします。 組織にこれらのグループに追加される独自のグループがある場合は、admin \tier 0 \groups OU に移動する必要があります。

    > [!NOTE]
    > グループは階層 0 の詳細については、「階層 0 の等価」を参照してください[特権アクセスのセキュリティで保護する参考資料](../securing-privileged-access/securing-privileged-access-reference-material.md)します。

4.  関連するグループに適切なメンバーを追加します。

    1.  **PAW ユーザー** - ドメインの階層 0 の管理者を追加または Enterprise Admin グループ手順 1 のフェーズ 1 で識別されます。

    2.  **PAW Maintenance** - PAW メンテナンスのために使用するには、少なくとも 1 つのアカウントを追加し、トラブルシューティング タスクを実行します。 PAW メンテナンス アカウントはほとんど使用されません。

        > [!NOTE]
        > PAW Users と PAW Maintenance の両方に同じユーザー アカウントまたはグループを追加することはできません。  PAW セキュリティ モデルは、自体が両方ではなくに、PAW ユーザー アカウントが PAW 上または管理対象システムに権限を権限が前提に一部基づいています。
        >
        > -   これは、適切な管理方法や習慣フェーズ 1 で構築するために重要です。
        > -   これは、フェーズ 2 および以降を通じて PAW 複数の階層にされている Paw を介した特権のエスカレーションを防ぐため、非常に重要です。
        >
        > 理想的には、担当者が、職務の分離の原則を適用する複数の階層で職務に割り当てられていないが、Microsoft が認識する多くの組織が制限されているスタッフ (またはその他の組織の要件) この完全分離しないようにします。 このような場合は、同じ人物が両方のロールに割り当てることができますが、これらの関数は、同じアカウントを使用しないでください。

5.  **"PAW Configuration-Computer"グループ ポリシー オブジェクト (GPO) および Tier 0 Devices OU へのリンクを作成する**(Tier 0 \admin の下の「デバイス」)。  このセクションで、新しい"PAW Configuration-Computer"これらの Paw の特定の保護を提供する GPO を作成します。

    > [!NOTE]
    > **これらの設定を既定のドメイン ポリシーに追加しない**します。  これを行うと、Active Directory 環境全体で操作は可能性のある影響します。  ここで説明している新しく作成された Gpo でのみこれらの設定を構成し、PAW OU にのみ適用します。

    1.  **PAW メンテナンス アクセス**- この設定は、paw は、特定のユーザー セットに特定の権限を持つグループのメンバーシップを設定します。 移動*コンピューターのコントロール パネル \ ユーザー*とグループと、次の手順に従ってください。

        1.  をクリックして**新規**] をクリック**ローカル グループ**

        2.  選択、**更新**操作、および ["Administrators (組み込み)"(使わないように、[参照] ボタンを Administrators ドメイン グループを選択) します。

        3.  選択、**すべてのメンバー ユーザーの削除**と**すべてのメンバー グループの削除**チェック ボックス

        4.  PAW メンテナンス (pawmaint) と管理者の追加 (、もう一度使用しない [参照] ボタンを管理者の選択) します。

            > [!NOTE]
            > ローカルの Administrators グループのメンバーシップの一覧に、PAW Users グループを追加しないでください。  PAW Users できません偶然または意図的に PAW 自体のセキュリティ設定、ローカルの Administrators グループのメンバーをすることがありますできません。

            グループ ポリシーの基本設定を使用してグループ メンバーシップを変更する方法については、TechNet の記事を参照してください[ローカル グループ] 項目を構成する](https://technet.microsoft.com/en-us/library/cc732525.aspx)します。

    2.  **ローカル グループのメンバーシップを制限する**-この設定は、ワークステーション上のローカル管理者グループのメンバーシップが常に空であることを確認

        1.  コンピューター [コントロール パネルの [ローカル ユーザーとグループに移動し、次の手順に従ってください。

            1.  をクリックして**新規**] をクリック**ローカル グループ**

            2.  選択、**更新**操作、および ["Backup Operators (組み込み)"(を使用して、[参照] ボタンを Backup Operators ドメイン グループを選択) します。

            3.  選択、**すべてのメンバー ユーザーの削除**と**すべてのメンバー グループの削除**チェック ボックスです。

            4.  グループにメンバーを追加しないでください。  クリックするだけで**OK**します。  空のリストを割り当てることによって、グループ ポリシーが自動的にすべてのメンバーを削除して空白のメンバーシップ一覧ごとにグループ ポリシーが更新されることが確認されます。

        2.  次の他のグループに対して上記の手順を完了します。

            -   暗号化演算子

            -   Hyper-V 管理者

            -   Network Configuration Operators

            -   パワー ユーザー

            -   リモート デスクトップ ユーザー

            -   レプリケーター

        3.  PAW Logon Restrictions - この設定は、PAW にログオンできるアカウントに制限されます。 この設定を構成するのには、次の手順に従います。

            1.  ローカル コンピューター ポリシー \windows 設定 \ セキュリティ \ ポリシー \ ユーザー権利の割り当てのログオンに移動します。

            2.  選択がこれらのポリシー設定を定義し、"PAW Users"と管理者の追加 (ここでも、使用しないで [参照] ボタンを管理者を選択) します。

        4.  **受信ネットワーク トラフィックをブロック**-この設定は、PAW に一方的な受信ネットワーク トラフィックは許可されないことを確認します。 この設定を構成するのには、次の手順に従います。

            1.  セキュリティが強化された高度な Security\Windows ファイアウォールされたポリシー \windows 設定 \ セキュリティ強化された windows ファイアウォールのコンピューターに移動し、次の手順に従ってください。

                1.  セキュリティが強化された Windows ファイアウォールを右クリックし、選択**ポリシーのインポート**します。

                2.  をクリックして**はい**、既存のファイアウォール ポリシーを上書きすることを受け入れるようにします。

                3.  PAWFirewall.wfw を参照して選択**開く**します。

                4.  をクリックして**OK**します。

                    > [!NOTE]
                    > 要請されていないトラフィックがこの時点で (例: セキュリティ スキャンまたは管理ソフトウェア PAW に到達する必要があるアドレスまたはサブネットを追加することがあります。
                    > WFW ファイル内の設定はすべてのファイアウォール プロファイル"ブロック-既定] モードでは、ファイアウォールを有効にする、ルールのマージをオフにして、パケットが破棄されたと成功の両方のログを有効にします。 これらの設定が承諾トラフィックをブロックは、PAW から開始された双方向通信が可しながらを防ぐローカル管理者のアクセスを持つユーザーは GPO 設定を上書きし、PAW との間のトラフィックを記録することを確認するローカル ファイアウォールの規則を作成します。
                    > **このファイアウォールを開くとは、PAW の攻撃対象領域を展開し、セキュリティ リスクが増大します。すべてのアドレスを追加するには、前にこのガイドで Managing and Operating PAW のセクションを参照してください。**します。

        5.  **Windows Update を WSUS の構成**-Paw の Windows Update を構成する設定を変更するのには、次の手順に従います。

            1.  コンピューターの構成 \ ポリシー \ 用テンプレート \windows コンポーネント \windows 更新プログラムに移動し、次の手順に従ってください。

                1.  有効にする、**自動更新を構成するポリシー**します。

                2.  オプションを選択**4 - 自動ダウンロードしインストール日時を指定**します。

                3.  オプションを変更**スケジュールされたインストール日**に**0 - 毎日**とオプション**スケジュールされたインストール時間**、組織の基本設定にします。

                4.  オプションを有効にする**イントラネット Microsoft 更新サービスの場所を指定**ポリシー、し、両方のオプションで ESAE WSUS サーバーの URL を指定します。

        6.  次のように、"PAW Configuration-Computer"GPO をリンクします。

            |ポリシー|リンク場所|
            |-----|---------|
            |PAW Configuration - コンピューター |Admin \tier 0 \devices|

6.  **"PAW Configuration-User"グループ ポリシー オブジェクト (GPO) および階層 0 のアカウント OU (Tier 0 \admin の下の「アカウント」) へリンクを作成する**します。  このセクションでは、新しい"PAW Configuration-User"これらの Paw の特定の保護を提供する GPO を作成します。

    > [!NOTE]
    > これらの設定を既定のドメイン ポリシーに追加しません。

    1.  **インターネットの閲覧をブロック**- 不注意によるインターネットの閲覧を阻止するループバック アドレス (127.0.0.1 のプロキシ アドレスを設定すると、)。

        1.  ユーザーの構成設定に移動します。 レジストリを右クリックし、選択**新規** \> **レジストリ項目**し、次の設定を構成します。

            1.  操作: 置換

            2.  ハイブ: HKEY_CURRENT_USER

            3.  キーのパス: software \microsoft\windows\currentversion\internet Settings

            4.  値の名前: ProxyEnable

                > [!NOTE]
                > 値の名前の左側の [既定] ボックスを選択しないでください。

            5.  値の種類: REG_DWORD

            6.  値のデータ: 1

                1.  します。  共通] タブをクリックし、選択**が適用されていない場合は、この項目を削除する**します。

                2.  [共通] タブで選択**アイテム レベル ターゲット設定**] をクリック**Targeting**します。

                3.  をクリックして**新しい項目**選択**セキュリティ グループ**します。

                4.  「...」ボタンをクリックし、PAW Users グループの [参照] を選択します。

                5.  をクリックして**新しい項目**選択**セキュリティ グループ**します。

                6.  「...」ボタンを選択し、参照、**Cloud Services Admins**グループ。

                7.  クリックして、**Cloud Services Admins** ] をクリックし、**項目のオプション**します。

                8.  選択**は**します。

                9. をクリックして**OK**ターゲット] ウィンドウにします。

            7.  をクリックして**OK** ProxyServer グループ ポリシー設定を完了するには

        2.  ユーザーの構成設定に移動します。 レジストリを右クリックし、選択**新規** \> **レジストリ項目**し、次の設定を構成します。

            -   操作: 置換

            -   ハイブ: HKEY_CURRENT_USER

            -   キーのパス: software \microsoft\windows\currentversion\internet Settings

            -   値の名前: ProxyServer

                > [!NOTE]
                > 値の名前の左側の [既定] ボックスを選択しないでください。

            -   値の種類: REG_SZ

            -   値のデータ: 127.0.0.1:80

                1.  をクリックして、**共通**] タブを選択**が適用されていない場合は、この項目を削除する**します。

                2.  **共通**] タブを選択**アイテム レベル ターゲット設定**] をクリック**Targeting**します。

                3.  をクリックして**新しい項目**および [セキュリティ グループ。

                4.  「...」ボタンを選択し、PAW Users グループを追加します。

                5.  をクリックして**新しい項目**および [セキュリティ グループ。

                6.  「...」ボタンを選択し、参照、**Cloud Services Admins**グループ。

                7.  クリックして、**Cloud Services Admins** ] をクリックし、**項目のオプション**します。

                8.  選択**は**します。

                9. をクリックして**OK**ターゲット] ウィンドウにします。

        3.  をクリックして**OK**、ProxyServer グループ ポリシー設定を完了するには

    2.  ユーザーの構成 \ ポリシー \ 用テンプレート \windows コンポーネント \internet Explorer に移動し、次のオプションを有効にします。 これらの設定すると、管理者がプロキシ設定を手動で上書きされなくなります。

        1.  有効にする、**自動構成の変更を許可しない**設定します。

        2.  有効にする、**プロキシ設定を変更できないようにする**します。

7.  **管理者を制限するによる下位階層のホストへのログオン**します。  このセクションでは、による下位階層のホストへのログオン権限を持つ管理者アカウントを防ぐためにグループ ポリシーを構成します。

    1.  作成、新しい**Restrict Workstation Logon** GPO - この設定は、制限階層 0 と階層 1 管理者アカウントが標準のワークステーションにログオンします。  この GPO は"Workstation"最上位レベル OU にリンクすることであり、次の設定。

        - (i) [バッチ ジョブとしてログオンにコンピューター ポリシー \windows 設定 \ セキュリティ \ ポリシー \ ユーザー権利の割り当て、次のように選択します。**これらのポリシー設定を定義する**階層 0 と階層 1 のグループを追加します。

            **グループ ポリシー設定を追加する]:**

            Enterprise Admins

            Domain Admins

            Schema Admins

            Domain \administrators

            アカウント オペレーター

            バックアップ オペレーター

            演算子を印刷します

            サーバー オペレーター

            ドメイン コント ローラー

            Read-Onlyドメイン コントローラー

            グループ ポリシーの作成者の所有者

            暗号化演算子

            > [!NOTE]
            > 注: 階層 0 のビルトイン グループ階層 0 と同等のグループの詳細を参照してください。

            その他の代理グループ

            > [!NOTE]
            > 注: 有効な階層 0 のアクセス権を持つグループを作成したカスタムでは、階層 0 と同等のグループの詳細を参照してください。

            階層 1 管理者

            > [!NOTE]
            > 注: このグループが作成されたフェーズ 1 で前

        - (ii) [コンピューター ポリシー \windows 設定 \ セキュリティ \ ポリシー \ ユーザー権利の割り当てとしてログオンをサービス、選択**これらのポリシー設定を定義する**階層 0 と階層 1 のグループを追加します。

            **グループ ポリシー設定を追加する]:**

            Enterprise Admins

            Domain Admins

            Schema Admins

            Domain \administrators

            アカウント オペレーター

            バックアップ オペレーター

            演算子を印刷します

            サーバー オペレーター

            ドメイン コント ローラー

            Read-Onlyドメイン コントローラー

            グループ ポリシーの作成者の所有者

            暗号化演算子

            > [!NOTE]
            > 注: 階層 0 のビルトイン グループ階層 0 と同等のグループの詳細を参照してください。

            その他の代理グループ

            > [!NOTE]
            > 注: 有効な階層 0 のアクセス権を持つグループを作成したカスタムでは、階層 0 と同等のグループの詳細を参照してください。

            に関する 1 Admins

            > [!NOTE]
            > 注: このグループが作成されたフェーズ 1 で前

    2.  作成、新しい**を制限するサーバーにログオン**GPO - この設定は、制限階層 0 の管理者アカウントが階層 1 のサーバーにログオンします。  この GPO は「Tier 1 Servers」の最上位レベル OU にリンクすることであり、次の設定。

        -   (i) [バッチ ジョブとしてログオンにコンピューター ポリシー \windows 設定 \ セキュリティ \ ポリシー \ ユーザー権利の割り当て、次のように選択します。**これらのポリシー設定を定義する**し、階層 0 のグループを追加します。

            **グループ ポリシー設定を追加する]:**

            Enterprise Admins

            Domain Admins

            Schema Admins

            Domain \administrators

            アカウント オペレーター

            バックアップ オペレーター

            演算子を印刷します

            サーバー オペレーター

            ドメイン コント ローラー

            Read-Onlyドメイン コントローラー

            グループ ポリシーの作成者の所有者

            暗号化演算子

            > [!NOTE]
            > 注: 階層 0 のビルトイン グループ階層 0 と同等のグループの詳細を参照してください。

            その他の代理グループ

            > [!NOTE]
            > 注: 有効な階層 0 のアクセス権を持つグループを作成したカスタムでは、階層 0 と同等のグループの詳細を参照してください。

        -   (ii) [コンピューター ポリシー \windows 設定 \ セキュリティ \ ポリシー \ ユーザー権利の割り当てとしてログオンをサービス、選択**これらのポリシー設定を定義する**し、階層 0 のグループを追加します。

            **グループ ポリシー設定を追加する]:**

            Enterprise Admins

            Domain Admins

            Schema Admins

            Domain \administrators

            アカウント オペレーター

            バックアップ オペレーター

            演算子を印刷します

            サーバー オペレーター

            ドメイン コント ローラー

            Read-Onlyドメイン コントローラー

            グループ ポリシーの作成者の所有者

            暗号化演算子

            > [!NOTE]
            > 注: 階層 0 のビルトイン グループ階層 0 と同等のグループの詳細を参照してください。

            その他の代理グループ

            > [!NOTE]
            > 注: 有効な階層 0 のアクセス権を持つグループを作成したカスタムでは、階層 0 と同等のグループの詳細を参照してください。

        -   (iii) [コンピューター ポリシー \windows 設定 \ セキュリティ \ \ 権利の割り当てログオンでローカルに、選択**これらのポリシー設定を定義する**し、階層 0 のグループを追加します。

            **グループ ポリシー設定を追加する]:**

            Enterprise Admins

            Domain Admins

            Schema Admins

            アカウント オペレーター

            バックアップ オペレーター

            演算子を印刷します

            サーバー オペレーター

            ドメイン コント ローラー

            Read-Onlyドメイン コントローラー

            グループ ポリシーの作成者の所有者

            暗号化演算子

            > [!NOTE]
            > 注: 階層 0 のビルトイン グループ階層 0 と同等のグループの詳細を参照してください。

            その他の代理グループ

            > [!NOTE]
            > 注: 有効な階層 0 のアクセス権を持つグループを作成したカスタムでは、階層 0 と同等のグループの詳細を参照してください。

8.  Paw を展開します。

    > [!NOTE]
    > オペレーティング システムの構築プロセス中に、PAW がネットワークから切断されていることを確認します。

    1.  前に入手したクリーン ソース インストール メディアを使用して Windows 10 をインストールします。

        > [!NOTE]
        > Microsoft Deployment Toolkit (MDT) または別の自動化されたイメージ展開システムを使用して、PAW の展開を自動化することがありますが、ビルド プロセスが、PAW と同等の信頼性を確認する必要があります。 敵対者特に探そうと企業のイメージおよび展開システム (Iso、展開パッケージなどを含む) を常設のメカニズムとしてため、既存の展開システムやイメージを使用しない必要があります。
        >
        > PAW の展開を自動化する場合は次の操作を行う必要があります。
        >
        > -   検証のガイダンスを使用して、インストール メディアを使用してシステムを構築[クリーン ソース インストール メディアの](http://aka.ms/cleansource)します。
        > -   オペレーティング システムの構築プロセス中に、自動展開システムがネットワークから切断されていることを確認します。

    2.  ローカルの Administrator アカウントの固有の複雑なパスワードを設定します。  環境内の他のアカウントのために使用されているパスワードは使用しません。

        > [!NOTE]
        > Microsoft を使用することをお勧め[ローカル管理者 Password Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899) Paw を含む、すべてのワークステーションのローカル管理者パスワードを管理します。  LAPS を使用する場合のみを付与すること、PAW Maintenance グループ パスワードを読み取る LAPS で管理された Paw の権利を確認します。

    3.  リモート サーバー管理ツールの Windows 10 のクリーン ソース インストール メディアを使用してをインストールします。

    4.  Enhanced Mitigation Experience Toolkit (EMET) クリーン ソース インストール メディアを使用してをインストールします。

        > [!NOTE]
        > このガイドの最終更新時に、EMET 5.5 がまだベータ テスト段階でが、注意してください。  これは Windows 10 でサポートされている最初のバージョンであるため、ことが含まれる次のとおり、ベータ状態にもかかわらずです。  リスク許容範囲を超えると、PAW にベータ ソフトウェアのインストール、現時点ではこの手順をスキップする可能性があります。

    5.  PAW をネットワークに接続します。  PAW が少なくとも 1 つのドメイン コントローラー (DC) に接続できることを確認します。

    6.  PAW Maintenance グループのメンバーであるアカウントを使用して、適切な OU 内のドメインに参加させますを新しく作成した PAW から次の PowerShell コマンドを実行します。

        `Add-Computer -DomainName Fabrikam -OUPath "OU=Devices,OU=Tier 0,OU=Admin,DC=fabrikam,DC=com"`

        参照を置き換える*Fabrikam*、ドメイン名を持つ適切です。  ドメイン名の複数のレベル (例: child.fabrikam.com) 場合、追加、追加する名前に、"DC ="識別子は、ドメインの完全修飾ドメイン名で表示される順序でします。

        > [!NOTE]
        > 展開した場合、[ESAE 管理フォレスト](http://aka.ms/esae)(フェーズ 1 で階層 0 の管理者) 用または[Microsoft Identity Manager (MIM) 特権アクセス管理 (PAM)](http://aka.ms/mimpamdeploy) (階層 1 と 2 の管理者フェーズ 2) は、その環境内の次のとおり、運用環境のドメインではなくドメインに PAW を参加させます. します。

    7.  ([管理ツール、エージェントなどを含む)。その他のソフトウェアをインストールする前にすべての重大かつ重要な Windows 更新プログラムを適用します。

    8.  グループ ポリシーの適用を強制します。

        1.  管理者特権のコマンド プロンプトを開き、次のコマンドを入力します。

            `Gpupdate /force /sync`

        2.  コンピューターを再起動します

    9. **(省略可能)** Active Directory 管理者の追加で必要なツールをインストールします。 他のツールやスクリプトの職務を実行するために必要をインストールします。 PAW に追加する前に、ツールによるターゲット コンピューターでの資格情報公開のリスクを評価することを確認します。 アクセス[このページ](http://aka.ms/logontypes)管理ツールと接続方法の資格情報漏洩リスクの評価に関する詳細情報を表示します。 ガイダンスを使用してすべてのインストール メディアを取得することを確認して[クリーン ソース インストール メディアの](http://aka.ms/cleansource)します。

        > [!NOTE]
        > これらのツールを一元化された場所のジャンプ サーバーを使用する場合でも、セキュリティ境界として機能しないことの複雑さの条件を削減できます。

    10. **(省略可能)**をダウンロードし、必要なリモート アクセス ソフトウェアをインストールします。 管理者を使用する場合、PAW リモートで管理のため、リモート アクセス ソリューション ベンダーからのセキュリティ ガイダンスを使用して、リモート アクセス ソフトウェアをインストールします。 インストール メディアのクリーン ソースのガイダンスを使用してすべてのインストール メディアを取得することを確認します。

        > [!NOTE]
        > 慎重に検討のすべてのリスクの PAW を介したリモート アクセスを許可することに関連します。  モバイル PAW は、在宅勤務など、多くの重要なシナリオの使用中にリモート アクセス ソフトウェア可能性のある攻撃に対して脆弱なでき、PAW を侵害するために使用します。

    11. ことをすべての適切な設定が代わりに、次の手順を使用していることを確認するには、PAW システムの整合性を検証します。

        1.  PAW に固有のグループ ポリシーのみが PAW に適用されていることを確認します。

            1.  管理者特権のコマンド プロンプトを開き、次のコマンドを入力します。

                `Gpresult /scope computer /r`

            2.  結果の一覧を確認し、唯一のグループを確実に表示されるポリシーは、上記で作成したものです。

        2.  追加のユーザー アカウントには、次の手順を使用して、PAW に特権グループのメンバーがないことを確認します。

            1.  開いている**編集のローカル ユーザーとグループ**(lusrmgr.msc)、select**グループ**、し、ローカルの Administrators グループのメンバーのみが、ローカルの管理者アカウントおよび PAW Maintenance グローバル セキュリティ グループがあることを確認します。

                > [!NOTE]
                > PAW Users グループには、ローカルの Administrators グループのメンバーができません。  メンバーだけが、ローカルの管理者アカウントおよび PAW Maintenance グローバル セキュリティ グループにする必要があります (および、PAW Users はそのグローバル グループのメンバーかも)。

            2.  使用しても**編集のローカル ユーザーとグループ**、次のグループにメンバーがないことを確認します。

                -   バックアップ オペレーター

                -   暗号化演算子

                -   Hyper-V 管理者

                -   Network Configuration Operators

                -   パワー ユーザー

                -   リモート デスクトップ ユーザー

                -   レプリケーター

    12. **(省略可能)**組織では、セキュリティ情報とイベント管理 (SIEM) ソリューションを使用している場合は、PAW がであることを確認[Windows イベント転送 (WEF) を使用してシステムにイベントを転送するように構成](http://blogs.technet.com/b/jepayne/archive/2015/11/24/monitoring-what-matters-windows-event-forwarding-for-everyone-even-if-you-already-have-a-siem.aspx)または登録されているソリューションでは、SIEM がアクティブに受信イベントおよび情報、PAW からできるようにします。  この操作の詳細については、SIEM ソリューションによって異なります。

        > [!NOTE]
        > SIEM エージェントが、Paw 上でシステム アカウントまたはローカル管理者アカウントとして実行する必要がある場合、ドメイン コントローラーおよび ID システムと同じ信頼レベルで、Siem が管理されていることを確認します。

    13. **(省略可能)**、PAW のローカル管理者アカウントのパスワードを管理する LAPS を展開して、選択した場合は、パスワードが正常に登録されていることを確認します。

        -   LAPS で管理されたパスワードを読み取るアクセス許可を持つアカウントを使用して開く**Active Directory ユーザーとコンピューター** (dsa.msc) します。  高度な機能が有効であり、適切なコンピューター オブジェクトを右クリックを確認します。  [属性エディター] タブを選択し、msSVSadmPwd の値が有効なパスワードにのみ含まれていることを確認します。

#### <a name="phase-2---extend-paw-to-all-administrators"></a>フェーズ 2 - すべての管理者への PAW の拡張
範囲: ミッション クリティカルなアプリケーションと依存関係経由で管理者権限を持つすべてのユーザー。  これは、少なくともアプリケーション サーバー、動作の正常性およびセキュリティ監視ソリューション、仮想化ソリューション、記憶域システム、およびネットワーク デバイスの管理者。

> [!NOTE]
> このフェーズの手順では、のでよく目フェーズ 1 が完了したことを前提としています。  すべてのフェーズ 1 で手順を完了するまでフェーズ 2 を開始しないでください。

すべての手順を実行したことを確認したら、フェーズ 2 を完了するには、次の手順を実行します。

1.  **(推奨)**を有効にする**RestrictedAdmin**モードでは、既存のサーバーおよびワークステーション上でこの機能を有効にし、この機能の使用を強制します。 この機能には、Windows Server 2008 R2 が実行されているターゲット サーバーは必要がありますまたはそれ以降にワークステーションを実行している Windows 7 以降をターゲットとします。

    1.  有効にする**RestrictedAdmin**モードで、サーバーおよびワークステーションで使用可能な」の手順に従って[ページ](http://aka.ms/rdpra)します。

        > [!NOTE]
        > インターネットに直接つながっているサーバーに対してこの機能を有効にする前に、敵対者が以前に盗んだパスワード ハッシュを使用してこれらのサーバーに認証を受けることのリスクを検討してください。

    2.  "RestrictedAdmin Required-Computer"グループ ポリシー オブジェクト (GPO) を作成します。 このセクションの使用を強制する GPO を作成する、/RestrictedAdmin 出力方向のリモート デスクトップ接続で、ターゲット システム上の資格情報の盗難からアカウントの保護を切り替える

        -   資格情報をリモート サーバーのコンピューターの構成 \ ポリシー \ システム \ 制限委任に移動し、設定**有効**します。

    3.  リンク、**RestrictedAdmin** Required - Computer を適切な階層 1 または下のポリシー オプションを使用して、階層 2 デバイス。

        PAW Configuration - コンピューター

        手順 -> link Location: admin \tier 0 \devices (既存)

        PAW 構成 - ユーザー

        手順 -> link Location: admin \tier 0\Accounts

        RestrictedAdmin が必要です] - コンピューター

        手順 -> admin \tier1\devices かの手順 -> admin \tier2\devices (どちらはも省略可能)

        > [!NOTE]
        > これは、これらのシステムは環境内のすべてのアセットの完全な制御が既に階層 0 のシステム必要はありません。

2.  階層 1 のオブジェクトを適切な Ou に移動します。

    1.  階層 1 のグループを admin \tier 1 \groups OU に移動します。 次の管理者権限を付与し、この OU に移動するすべてのグループを見つけます。

        -   複数のサーバー上のローカル管理者

        -   クラウド サービスへの管理アクセス

        -   エンタープライズ アプリケーションへの管理アクセス

    2.  階層 1 のアカウントを admin \tier 1\Accounts OU に移動します。 この OU にそれらの階層 1 グループ (入れ子になったメンバーシップを含む) のメンバーである各アカウントに移動します。

3.  関連するグループに適切なメンバーを追加します。

    -   **Tier 1 Admins** -このグループには、階層 2 のホストへのログオンが制限されている階層 1 の管理者にが含まれます。 すべてのサーバーまたはインターネット サービス経由で管理者特権を持つ階層 1 管理者グループを追加します。

        > [!NOTE]
        > 管理担当者の職務を複数の階層で資産を管理する場合は、階層ごとに個別の管理アカウントを作成する必要があります。

4.  資格情報の盗難のリスクを低減し、再利用する Credential Guard を有効にします。  Credential Guard は、資格情報をアプリケーションへのアクセスを制限する (Pass the Hash を含む) の資格情報盗難攻撃を阻止 Windows 10 の新しい機能です。  Credential Guard はエンド ユーザーに対して完全に透過的し、最小限のセットアップの時間と労力が必要です。  展開の手順やハードウェア要件などの Credential Guard の詳細については、記事を参照してください[Credential Guard によるドメインの資格情報の保護](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx)します。

    > [!NOTE]
    > 構成して Credential Guard を使用するためには、device Guard を有効にする必要があります。  ただし、Credential Guard を使用するためにその他の Device Guard の保護を構成する必要はありません。

5.  **(省略可能)**クラウド サービスへの接続を有効にします。 この手順では、適切なセキュリティ保証と Azure や Office 365 などのクラウド サービスの管理ができます。 この手順は、Microsoft Intune で Paw を管理するために必要もあります。

    > [!NOTE]
    > Intune でのクラウド サービスと管理の管理に必要なクラウド接続がない場合は、この手順を省略します。

    次の手順では、承認されたクラウド サービスのみにインターネット (ただし、オープンなインターネットしない) 経由で通信を制限し、保護、ブラウザーとは、インターネットからコンテンツを処理する他のアプリケーションを追加します。 インターネット通信や生産性向上などの標準ユーザー タスク、これらの Paw の管理を使用しないください。

    サービスを PAW への接続を有効にするには、次の手順に従います。

    1.  承認されたインターネット送信先のみを許可するように PAW を構成します。  クラウドの管理を有効にする、PAW の展開を拡張すると、オープンなインターネットからのアクセスをフィルタ リング、ここで攻撃より簡単にマウントできます管理者に対して承認されたサービスへのアクセスを許可するようにする必要があります。

        1.  作成**Cloud Services Admins**グループ化し、すべてのアカウントを追加するには、インターネット上のクラウド サービスへのアクセスを必要としています。

        2.  PAW のダウンロード*proxy.pac*ファイルから[TechNet ギャラリー](http://aka.ms/pawmedia)内部の Web サイトで公開します。

            > [!NOTE]
            > 更新する必要があります、*proxy.pac*を完全な最新の状態であることを確認するダウンロード後にファイルをします。  
            > Microsoft Office 内の現在のすべての Office 365 と Azure の Url を発行[サポート センター](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US)します。
            >
            > その他の有効なインターネットの出力先の他の IaaS プロバイダーでは、この一覧に追加が、追加の生産性、エンターテインメント、ニュース、またはこの一覧にサイトを検索を追加する必要があります。
            >
            > また、これらのアドレスを使用する有効なプロキシ アドレスをように PAC ファイルを調整する必要があります。

            > [!NOTE]
            > 多層防御の Web プロキシを使用しても、PAW からのアクセスを制限することもできます。 使用してこれを単独で PAC ファイルがないように、企業ネットワークに接続されているときの Paw に対するアクセスを制限することはのみお勧めしません。

            これらを前提と Internet Explorer (または Microsoft Edge) を使用して、Office 365、Azure、およびその他のクラウド サービスの管理します。 管理に必要なすべてのサード パーティ ブラウザーに対して同様の制限を構成することをお勧めします。 Paw 上の Web ブラウザーは、クラウド サービスの管理、決して全般的な Web の閲覧にのみ使用できます。

        3.  構成した後、*proxy.pac*ファイルを PAW Configuration - User GPO を更新します。

            1.  ユーザーの構成設定に移動します。 レジストリを右クリックし、選択**新規** \> **レジストリ項目**し、次の設定を構成します。

                1.  操作: 置換

                2.  ハイブ: HKEY_ 現在のユーザー

                3.  キーのパス: software \microsoft\windows\currentversion\internet Settings

                4.  値の名前: AutoConfigUrl

                    > [!NOTE]
                    > 選択しないでください、**既定**値の名前の左側にあるボックス。

                5.  値の種類: REG_SZ

                6.  値のデータ: 完全な URL を入力、*proxy.pac* http:// とファイル名 - http://proxy.fabrikam.com/proxy.pac などを含むファイル。  URL には、単一ラベルの URL - たとえば、http://proxy/proxy.pac ことができます。

                    > [!NOTE]
                    > PAC ファイルは、file://server.fabrikan.com/share/proxy.pac の構文を使用して、ファイル共有でホストすることもできますが、file:// プロトコルを許可する必要があります。 この「注:: File://-based プロキシ スクリプト非推奨」セクションを参照して[Understanding Web プロキシ構成](http://blogs.msdn.com/b/ieinternals/archive/2013/10/11/web-proxy-configuration-and-ie11-changes.aspx)必要なレジストリ値の構成の詳細については、ブログします。

                7.  をクリックして、**共通**] タブを選択**が適用されていない場合は、この項目を削除する**します。

                8.  **共通**] タブを選択**アイテム レベル ターゲット設定**] をクリック**Targeting**します。

                9. をクリックして**新しい項目**選択**セキュリティ グループ**します。

                10. 「...」ボタンを選択し、参照、**Cloud Services Admins**グループ。

                11. をクリックして**新しい項目**選択**セキュリティ グループ**します。

                12. 「...」ボタンを選択し、参照、**PAW Users**グループ。

                13. クリックして、**PAW Users** ] をクリックし、**項目のオプション**します。

                14. 選択**は**します。

                15. をクリックして**OK**ターゲット] ウィンドウにします。

                16. をクリックして**OK**を完了する、**AutoConfigUrl**ポリシー設定をグループ化します。

    2.  Windows 10 セキュリティ ベースラインおよびクラウド サービス アクセス リンク Windows およびクラウド サービスのセキュリティ基本計画 (必要な場合) にアクセスが次の手順を使用して適切な Ou に適用されます。

        1.  Windows 10 Security Baselines ZIP ファイルの内容を抽出します。

        2.  これらの Gpo の作成[ポリシーをインポート](https://technet.microsoft.com/en-us/library/cc753786.aspx)設定、および[リンク](https://technet.microsoft.com/en-us/library/cc732979.aspx)下の表に従ってします。 それぞれの場所に各ポリシーをリンクし、表の順番に従って (下の表にあるエントリが適用された後より高い優先順位である必要があります)。

            **ポリシー:**

            |||
            |-|-|
            |CM の Windows 10: ドメインのセキュリティ|該当なし - ここではリンクしません|
            |SCM Windows 10 TH2 - コンピューター|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |SCM Windows 10 TH2-BitLocker|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |SCM Windows 10 の Credential Guard|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |SCM Internet Explorer - コンピューター|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |PAW Configuration - コンピューター|Admin \tier 0 \devices (既存)|
            ||Admin \tier 1\Devices (新しいリンク)|
            ||Admin \tier 2 \devices (新しいリンク)|
            |RestrictedAdmin が必要です] - コンピューター|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |SCM Windows 10 のユーザー|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |SCM Internet Explorer - ユーザー|Admin \tier 0 \devices|
            ||Admin \tier 1\Devices|
            ||Admin \tier 2 \devices|
            |PAW 構成 - ユーザー|Admin \tier 0 \devices (既存)|
            ||Admin \tier 1\Devices (新しいリンク)|
            ||Admin \tier 2 \devices (新しいリンク)|

            > [!NOTE]
            > "SCM Windows 10-Domain Security"GPO は、PAW とは別のドメインにリンクすることがありますが、ドメイン全体に影響を与えます。

6.  **(省略可能)**階層 1 の管理者の追加で必要なツールをインストールします。 他のツールやスクリプトの職務を実行するために必要をインストールします。 PAW に追加する前に、ツールによるターゲット コンピューターでの資格情報公開のリスクを評価することを確認します。 資格情報漏洩リスクのメソッドを参照してください [管理ツールと接続の評価の詳細については[このページ](http://aka.ms/logontypes)します。 インストール メディアのクリーン ソースのガイダンスを使用してすべてのインストール メディアを取得することを確認します。

7.  識別し、ソフトウェアと管理に必要なアプリケーションを安全に取得します。  これは、アプリケーション、サービス、およびセキュリティで保護されたシステムの数が増えるためより広範なスコープを持つが、フェーズ 1 で実行される作業に似ています。

    > [!NOTE]
    > これらの新しいアプリケーション (Web ブラウザーを含む) を保護することを確認して無効にするには、EMET によって提供される保護します。

    追加のソフトウェアとアプリケーションの例は次のとおりです。

    -   Microsoft Azure PowerShell

    -   Office 365 PowerShell (とも呼ばれる Microsoft Online Services モジュール)

    -   アプリケーションまたは Microsoft 管理コンソールに基づいてサービス管理ソフトウェア

    -   独自の (非 MMC ベースの) アプリケーションまたはサービスの管理ソフトウェア

        > [!NOTE]
        > 多くのアプリケーションはのみなど多くのクラウド サービスの Web ブラウザーで管理されてようになりました。  これにより、PAW にインストールする必要があるアプリケーションの数、ブラウザーの相互運用性の問題のリスクも紹介します。  特定のサービスの管理を有効にする特定の PAW インスタンス上に Microsoft 以外の Web ブラウザーを展開する必要があります。  追加の Web ブラウザーを展開する場合は、すべてのクリーン ソースの原則に従いますして、ベンダーのセキュリティのガイダンスに従って、ブラウザーをセキュリティで保護することを確認します。

8.  **(省略可能)**ダウンロードし、必要な管理エージェントをインストールします。

    > [!NOTE]
    > 追加の管理エージェント (監視、セキュリティ、構成管理など) をインストールする場合は、ドメイン コントローラーおよび ID システムと同じレベルで管理システムが信頼されていることを確認する必要があります。 詳細なガイダンスについては、管理および Paw の更新を参照してください。

9. PAW によって提供される追加のセキュリティ保護を必要とするシステムを識別する、インフラストラクチャを評価します。  どのシステムを保護する必要が正確に理解していることを確認します。  重要なに関する質問、自分自身のリソースなど。

    -   管理する必要がある対象のシステムはどこですか。  1 つの物理的な場所に収集または明確に定義された 1 つのサブネットに接続されているか。

    -   システムの数はありますか。

    -   他のシステム (仮想化、記憶域など) に依存してこれらのシステムと必要な場合は、これらのシステムを管理する方法ですか。  方法はこれらの依存関係、およびその他のリスクに公開されている重要なシステムに関連付けられているこれらの依存関係ですか。

    -   重要度、管理されているサービスとそれらのサービスが侵害された場合は、予想される損失ですか。

        > [!NOTE]
        > この評価でクラウド サービスを含めて - 攻撃者が安全でないクラウドに展開をますますターゲットそうしていただけると、オンプレミスのミッションクリティカルなアプリケーションの場合と安全にそれらのサービスを管理することが重要です。

        この評価を使用して、追加の保護を必要とする特定のシステムを識別し、これらのシステムの管理者に、PAW プログラムを拡張します。  PAW ベースの管理によって大きなメリット システムの一般的な例としてには、SQL Server (、オンプレミスと SQL Azure の両方)、人事アプリケーション、および財務ソフトウェアが含まれます。

        > [!NOTE]
        > Windows システム リソースを管理する場合は、Windows 以外のオペレーティング システム、またはマイクロソフト以外のクラウド プラットフォームで、アプリケーション自体が実行される場合でも、PAW を使用管理できます。  たとえば、Amazon Web Services サブスクリプションの所有者はそのアカウントを管理、PAW を使用する必要がありますのみ。

10. 組織の規模で Paw を展開するための要求と配布方法を開発します。  フェーズ 2 で展開を選択した Paw の数、によって、プロセスを自動化する必要があります。

    -   正式な要求と承認のプロセスを使用して、PAW を取得する管理者の開発を検討してください。  このプロセスは、展開プロセスの標準化、PAW デバイスの信頼性の確保および PAW の展開内のギャップを識別するために役立ちます。

    -   前述のように、この展開ソリューションは既存の自動化方法 (これは既に侵害されて) 別にする必要があり、フェーズ 1 で説明した原則に従う必要があります。

        > [!NOTE]
        > 同じかそれ以上の信頼レベルでリソースを管理するすべてのシステムを管理自体必要があります。

11. 確認し、必要な場合は、追加の PAW ハードウェア プロファイルを展開します。  フェーズ 1 の展開を選択したハードウェア プロファイルは、すべての管理者に適さない場合があります。  ハードウェア プロファイルを確認し、該当する場合は、管理者のニーズに合わせて追加の PAW ハードウェア プロファイルを選択します。  たとえば、Dedicated Hardware プロファイル (別の PAW と日常的使用されるワークステーション) ない可能性があります出張が多い管理者に適した - ここでは、その管理者用に Simultaneous Use プロファイル (PAW ユーザー VM) を展開する選択した可能性があります。

12. カルチャ、運用、通信、およびを拡張の PAW の展開を伴うトレーニングのニーズを検討してください。   管理モデルに大きな変更はある程度の変更管理が必要自然と、展開プロジェクト自体に組み込むことに不可欠です。  次の最低限考慮します。

    -   変更をサポートされることを確認する上級管理者の支援をやり取りする方法は、ですか。  上級管理者の支援が、失敗する可能性がないプロジェクトまたは資金の確保少なくとも非常に困難にや広範囲の同意します。

    -   ドキュメント化する方法、新しいプロセスの管理者ですか。  これらの変更を文書化されているし、既存管理者 (慣習を変更する必要がありますおよび別の方法でリソースを管理)、するだけでなく、新しい管理者 (組織外から雇用されたり内から昇格) にも伝達する必要があります。  マニュアルはオフになっており、重要性、脅威の管理者、および PAW の正しい使用する方法を保護するうえでの PAW の役割を明確に説明が重要です。

        > [!NOTE]
        > これは、ロールと高い回転、ヘルプ デスク担当者に限定されませんを含むために特に重要です。

    -   どのように、新しいプロセスに準拠しますか。  PAW モデルには、さまざまな特権を持つ資格情報の漏洩を防ぐために技術的なコントロールが含まれているときに、純粋な技術的制御を使用してすべての露出の可能性を完全に防ぐことはできません。  たとえば、ことができますが、管理者が特権を持つ資格情報を持つユーザーのデスクトップに正常にログオンするを防ぐため、ログオンしようとした単純な act はそのユーザーのデスクトップにインストールされているマルウェアに資格情報を公開できます。  したがって、ことを明確に定義が、PAW モデルのメリットだけでなく、非対応のリスクが不可欠です。  これはこれを補足する、監査、アラートができるように、資格情報の公開をすばやく検出および修正しました。

#### <a name="phase-3-extend-and-enhance-protection"></a>フェーズ 3: 拡張し、保護を強化
範囲: このような保護は、多要素認証やネットワーク アクセス ルールを含む高度な機能と基本的な保護を強化、フェーズ 1 で構築したシステムを強化します。

> [!NOTE]
> このフェーズは、フェーズ 1 が完了した後、いつでも実行できます。  フェーズ 2 の完了に依存していないし、実行する前に、フェーズ 2 の前後で、同時に、したがってすることができます。

このフェーズを構成するのには、次の手順に従います。

1.  特権アカウントの多要素認証を有効にします。  多要素認証は、資格情報だけでなく物理的なトークンを提供するように求めることで、アカウントのセキュリティを強化します。  多要素認証が非常にも、認証ポリシーを補完が、認証ポリシーの展開には依存しません (および同様に、認証ポリシーには多要素認証は不要)。  これらの形式の多要素認証のいずれかの方法をお勧めします。

    -   **スマート カード**: スマート カードは、Windows ログオン プロセス中に 2 番目の確認を提供するための改ざんされにくいポータブル物理デバイスです。  ログオン用のカードを所有する個人を要求することでは、リモートで再利用される資格情報を盗まれたりした場合のリスクを軽減できます。  Windows でのスマート カード ログオンについて詳しくを参照してください、記事[スマート カードの概要](https://technet.microsoft.com/en-us/library/hh831433.aspx)します。

    -   **仮想スマート カード**: 仮想スマート カードは物理的なスマート カードの特定のハードウェアにリンクされているというメリットと同じセキュリティ上の利点を提供します。  展開およびハードウェア要件の詳細についてを参照してください、記事[仮想スマート カードの概要](https://technet.microsoft.com/en-us/library/dn593708.aspx)と[仮想スマート カードの概要: チュートリアル ガイド](https://technet.microsoft.com/en-us/library/dn579260.aspx)します。

    -   **Microsoft Passport**: Microsoft Passport ではユーザーの Microsoft アカウント、Active Directory アカウント、Microsoft Azure Active Directory (Azure AD) アカウント、または Fast ID Online (FIDO) 認証をサポートする Microsoft 以外のサービスに認証します。 2 段階の初期検証の後 Microsoft Passport 登録時に、Microsoft Passport がユーザーのデバイスにセットアップし、ユーザーが、ジェスチャーになる可能性が Windows Hello または PIN を設定します。 Microsoft Passport の資格情報は、非対称キー ペアであり、トラステッド プラットフォーム モジュール (Tpm) の分離環境内で生成されることができます。
        Microsoft Passport の詳細についてを参照[Microsoft Passport の概要](https://technet.microsoft.com/en-us/library/dn985839%28v=vs.85%29.aspx)記事です。

    -   **Azure 多要素認証**: Azure 多要素認証 (MFA) は、2 つ目の検証要素だけでなく監視とマシン学習ベースの分析によって強化された保護のセキュリティを提供します。  Azure MFA は、Azure 管理者だけでなく他の多くのソリューションも、Web アプリケーション、Azure Active Directory、リモート アクセスとリモート デスクトップのようなオンプレミス ソリューションなどを保護できます。  Azure の multi-factor authentication について詳しくを参照してください、記事[Multi-factor Authentication](https://azure.microsoft.com/en-us/services/multi-factor-authentication)します。

2.  **信頼された Device Guard や AppLocker を使用してアプリケーションのホワイト リスト**します。  信頼されていないか、署名されていないコードの PAW 上で実行する機能を制限すると、悪意のあるアクティビティやセキュリティ侵害が発生する可能性をさらに削減します。  Windows には、2 つのプライマリ アプリケーション制御オプションが含まれています。

    -   **AppLocker**: AppLocker が特定のシステムで実行できるアプリケーション管理者の制御に役立ちます。  AppLocker を一元的に、グループ ポリシーによって制御および (Paw のユーザーを対象となるアプリケーション) の特定のユーザーまたはグループに適用できます。  AppLocker について詳しくは、TechNet の記事を参照してください[AppLocker の技術概要](https://technet.microsoft.com/library/hh831440.aspx)します。

    -   **Device Guard**: Device Guard の新機能については、強化されたハードウェア ベースのアプリケーション コントロールをオーバーライドことはできません、AppLocker とは異なり、影響を受けるデバイス。  、AppLocker と同様に、Device Guard をグループ ポリシーを使用して制御および特定のユーザーを対象とすることができます。  Device Guard とアプリケーションの使用率の制限の詳細については、TechNet の記事を参照してください[Device Guard 展開ガイド](https://technet.microsoft.com/en-us/library/mt463091(v=vs.85).aspx)します。

3.  **Protected Users、認証ポリシーと認証サイロを使用して、さらに権限を持つアカウントを保護する**します。  Protected Users のメンバーは、資格情報を保護する追加のセキュリティ ポリシーの対象は、ローカル セキュリティ エージェント (LSA) に格納され、大幅に資格情報の盗難および再利用のリスクを最小限に抑えます。  認証ポリシーとサイロは、どの特権を持つユーザーを制御、ドメイン内のリソースにアクセスできます。  集合的に、このような保護では、これらの特権を持つユーザー アカウントのセキュリティを大幅に強化します。  これらの機能について詳しくを参照してください、Web の記事[保護されるアカウントの構成方法](https://technet.microsoft.com/en-us/library/dn518179.aspx)します。

    > [!NOTE]
    > このような保護を意図するものを補完、置き換えられることは、既存のフェーズ 1 でのセキュリティ対策です。  でも、管理者は、管理と一般的な用途は個別のアカウントを使用する必要があります。

### <a name="managing-and-updating-paws"></a>Paw の管理と更新
Paw のマルウェア対策機能を必要し、これらのワークステーションの整合性を維持するために、ソフトウェアの更新を迅速に適用する必要があります。

追加の構成管理、運用監視、およびセキュリティ管理も使用できます、Paw と共にが各管理機能のツールを介して PAW が侵害されるリスクがあるために、これらの統合をについて慎重に検討する必要があります。 かどうか、導入に意味の高度な管理機能は、さまざまな要因によって異なります。

-   セキュリティの状態と管理機能 (これらの役割、オペレーティング システム、ツールがホストまたはから、管理およびその他のハードウェアまたはソフトウェアの依存関係をツールで、ツール、管理者の役割とアカウントのソフトウェアの更新方法を含む) のプラクティス

-   頻度とソフトウェアの展開と Paw 上で更新プログラムの数

-   インベントリと構成に関する詳細情報の要件

-   セキュリティ監視要件

-   組織の標準とその他の組織固有の要素

クリーン ソースの原則ごと管理または Paw を監視するために使用するすべてのツールは、Paw のレベルを以上に信頼されたする必要があります。 これには、これらのツールを権限の低いワークステーションからセキュリティの依存関係がないことを確認する PAW から管理する通常必要があります。

管理し、監視、Paw に使用できるいくつかの方法の概要を次の表に示します。

|アプローチ|考慮事項|
|------|---------|
|PAW を既定します。<br /><br />Windows Server Update Services<br />Windows Defender|-追加コスト<br />-必要なセキュリティの基本的な機能を実行します。<br />のこのガイドに記載手順|
|管理[Intune](https://technet.microsoft.com/en-us/library/jj676587.aspx)|<ul><li>クラウド ベースの可視性と制御を提供します。<br /><br /><ul><li>ソフトウェアの展開</li><li>O ソフトウェア更新プログラムの管理</li><li>Windows ファイアウォール ポリシーの管理</li><li>マルウェア対策の保護</li><li>リモート アシスタンス</li><li>ソフトウェア ライセンス管理します。</li></ul></li><li>サーバー インフラストラクチャは必要ありません。</li><li>フェーズ 2 の「を有効に接続するクラウド サービス」の手順に従う必要があります。</li><li>PAW コンピューターがドメインに参加していない場合、は、セキュリティ ベースラインのダウンロードで提供されるツールを使用してローカル イメージに、SCM ベースラインを適用する必要があります。</li></ul>|
|Paw を管理するための新しい System Center インスタンス|-可視性と構成、ソフトウェアの展開、およびセキュリティ更新プログラムの制御を提供します<br />-個別のサーバー インフラストラクチャ、Paw、レベルのセキュリティで保護して、高い特権のある人物のスキルが必要です。|
|既存の管理ツールの Paw を管理します。|-既存の管理インフラストラクチャは、Paw のセキュリティ レベルになる場合を除き、Paw のセキュリティを侵害する重大なリスクを作成する**注:** Microsoft は、組織にそれを使用する特定の理由がない限り、このアプローチ防止一般にします。 経験が通常はこれらのツール (およびのセキュリティの依存関係) のすべての移行の非常に高いコスト、Paw のセキュリティ レベルまでです。<br />のこれらのツールのほとんど可視性と構成、ソフトウェアの展開、およびセキュリティ更新プログラムの制御を提供します。|
|セキュリティ スキャンまたは管理者のアクセスを必要とするツールの監視|エージェントをインストールまたはローカル管理者のアクセスを持つアカウントを必要とするツールが含まれます。<br /><br />-Paw レベルの最大ツールのセキュリティ保証を戻すことが必要です。<br />-場合がありますツールの機能をサポートするために Paw のセキュリティ体制を下げる (ポートを開く、Java または他のミドルウェアなどのインストール)、セキュリティのトレードオフの意思決定を作成します。|
|セキュリティ情報とイベント管理 (SIEM)|<ul><li>SIEM がエージェントレスの場合<br /><br /><ul><li>アカウントを使用して管理者アクセス権のない Paw 上のイベントにアクセスできる、**Event Log Readers**グループ</li><li>SIEM サーバーからの着信トラフィックを許可するように、ネットワーク ポートを開く必要があります。</li></ul></li><li>エージェントが SIEM に必要な場合は、その他の行を参照してください**セキュリティ スキャンまたは管理者のアクセスを必要とするツールを監視**します。</li></ul>|
|Windows イベント転送|-Paw から外部コレクターまたは SIEM にセキュリティ イベントを転送のエージェントレスの方法を提供します。<br />-イベントは、Paw に管理アクセス権を持たないアクセスできます。<br />に SIEM サーバーからの着信トラフィックを許可するようにネットワーク ポートを開くは必要ありません。|

#### <a name="operating-paws"></a>Paw の運用
標準を使用して、PAW ソリューションを運用する必要があります[運用基準](http://aka.ms/securitystandards)クリーン ソースの原則に基づいています。

## <a name="related-topics"></a>関連するトピック
[魅力的な Microsoft Cybersecurity サービスします。](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)

[プレミアの特長: Pass the Hash やその他の資格情報の盗難を軽減する方法](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced Threat Analytics](http://aka.ms/ata)

[Credential Guard によるドメインの派生資格情報を保護します。](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx)

[Device Guard の概要](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx)

[セキュリティで保護された管理ワークステーションを高価値資産を保護します。](https://msdn.microsoft.com/en-us/library/mt186538.aspx)

[Dave Probert による (Channel 9)、Windows 10 の分離ユーザー モード](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[ユーザー モード プロセスと Logan による Windows 10 の機能を分離 Gabriel (Channel 9)](http://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[プロセスと Dave Probert (Channel 9) による Windows 10 の分離ユーザー モードで機能の詳細](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Windows 10 分離ユーザー モード (Channel 9) を使用して資格情報の盗難の軽減](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Windows Kerberos での KDC の厳密な検証を有効にします。](https://www.microsoft.com/en-us/download/details.aspx?id=6382)

[Windows Server 2012 の Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)

[Windows Server 2008 R2 で AD DS の認証メカニズム保証 Step-by-Step Guide](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[トラステッド プラットフォーム モジュール](C:\sd\docs\p_ent_keep_secure\p_ent_keep_secure\trusted_platform_module_technology_overview.xml)
