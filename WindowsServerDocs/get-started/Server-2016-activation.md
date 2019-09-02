---
title: Microsoft サーバーのライセンス認証
description: Windows Server 2016 をライセンス認証する方法。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 09/19/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a45d5cc7a54
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 88cab1965e299c7d25c177125cb504432bf987e8
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "66810651"
---
# <a name="windows-server-2016-activation"></a>Windows Server 2016 のライセンス認証

ここでは、Windows Server 2016 が関係するキー管理サービス (KMS) ライセンス認証を計画する場合の最初の考慮事項について説明します。 ここに挙げられたものより古いオペレーティング システムが関係する KMS ライセンス認証については、「[手順 1: ライセンス認証方法の確認と選択](https://technet.microsoft.com/library/jj134256(WS.11).aspx)」をご覧ください。

KMS では、クライアント/サーバー モデルを使用してクライアントのライセンス認証を行います。 KMS クライアントは、ライセンス認証を行うために、KMS ホストと呼ばれる KMS サーバーに接続します。 KMS ホストは、ローカル ネットワーク上に存在する必要があります。

KMS ホストは、専用サーバーである必要はありません。KMS は、他のサービスと共存させることができます。 KMS ホストは、Windows 10、Windows Server 2016、Windows Server 2012 R2、Windows 8.1、または Windows Server 2012 が実行されている任意の物理システムまたは仮想システムで実行できます。

Windows 10 または Windows 8.1 上で実行されている KMS ホストは、クライアント オペレーティング システムが実行されているコンピューターのみライセンス認証できます。
次の表は、Windows Server 2016 および Windows 10 のクライアントを含んだネットワークの、KMS ホストおよびクライアントの要件をまとめたものです。

> [!NOTE]
> **注:** ここに挙げた比較的新しいクライアントでは、ライセンス認証をサポートするために KMS サーバーの更新が必要になることがあります。 ライセンス認証のエラーが発生したときは、この表の下に示した適切な更新プログラムを適用してあるかどうかを確認してください。

|プロダクト キー グループ|KMS をホストできるオペレーティング システム|この KMS ホストによってライセンス認証される Windows エディション|  
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|  
|Windows Server 2016 のボリューム ライセンス|Windows Server 2012<br /><br />Windows Server 2012 R2<br /><br />Windows Server 2016<br /><br />|Windows Server 半期チャネル <br><br>Windows Server 2016 (すべてのエディション)<br /><br />Windows 10 LTSB (2015 および 2016)<br /><br />Windows 10 Professional<br /><br />Windows 10 Enterprise<br /><br />Windows 10 Pro for Workstations<br><br>Windows 10 Education<br><br>Windows Server 2012 R2 (すべてのエディション)<br /><br />Windows 8.1 Professional<br /><br />Windows 8.1 Enterprise<br /><br />Windows Server 2012 (すべてのエディション)<br /><br />Windows Server 2008 R2 (すべてのエディション)<br /><br />Windows Server 2008 (すべてのエディション)<br /><br />Windows 7 Professional<br /><br />Windows 7 Enterprise| 
|Windows 10 のボリューム ライセンス|Windows 7<br /><br />Windows 8.1<br /><br /> Windows 10|Windows 10 Professional<br /><br /> Windows 10 Professional N<br /><br /> Windows 10 Enterprise<br /><br /> Windows 10 Enterprise N<br /><br /> Windows 10 Education<br /><br /> Windows 10 Education N<br /><br /> Windows 10 Enterprise LTSB (2015)<br /><br /> Windows 10 Enterprise LTSB N (2015)<br /><br /> Windows 10 Pro for Workstations<br><br>Windows 8.1 Professional<br /><br /> Windows 8.1 Enterprise<br /><br /> Windows 7 Professional<br /><br /> Windows 7 Enterprise<br /><br />|  
|"Windows Server 2012 R2 for Windows 10" のボリューム ライセンス|Windows Server 2008 R2<br /><br /> Windows Server 2012 Standard<br /><br /> Windows Server 2012 Datacenter<br /><br /> Windows Server 2012 R2 Standard<br /><br />Windows Server 2012 R2 Datacenter|Windows 10 Professional<br /><br /> Windows 10 Enterprise<br /><br />Windows 10 Enterprise LTSB (2015)<br><br>Windows 10 Pro for Workstations<br><br>Windows 10 Education<br><br> Windows Server 2012 R2 (すべてのエディション)<br /><br /> Windows 8.1 Professional<br /><br /> Windows 8.1 Enterprise<br /><br /> Windows Server 2012 (すべてのエディション)<br /><br /> Windows Server 2008 R2 (すべてのエディション)<br /><br />Windows Server 2008 (すべてのエディション)<br /><br /> Windows 7 Professional<br /><br /> Windows 7 Enterprise|

> [!NOTE]  
> KMS サーバーが実行しているオペレーティング システムや、ライセンス認証するオペレーティング システムによっては、次の更新プログラムのいくつかをインストールすることが必要になる場合があります。
> - Windows 10 を実行しているクライアントのライセンス認証をサポートするには、Windows 7 および Windows Server 2008 R2 にインストールされている KMS を更新する必要があります。 詳しくは、 [Windows 7 と Windows Server 2008 R2 KMS のホストで Windows 10 のライセンス認証を可能にする更新プログラム](https://support.microsoft.com/help/3079821/update-that-enables-windows-7-and-windows-server-2008-r2-kms-hosts-to-activate-windows-10)に関するページをご覧ください。  
> - Windows 10 と Windows Server 2016、またはそれ以降のクライアントまたはサーバー オペレーティング システムを実行しているクライアントのライセンス認証をサポートするには、Windows Server 2012 にインストールされている KMS を更新する必要があります。 詳しくは、 [Windows Server 2012 の 2016 年 7 月の更新プログラムのロールアップ](https://support.microsoft.com/help/3172615/july-2016-update-rollup-for-windows-server-2012)に関するページをご覧ください。 
> - Windows 10 と Windows Server 2016、またはそれ以降のクライアントまたはサーバー オペレーティング システムを実行しているクライアントのライセンス認証をサポートするには、Windows 8.1 または Windows Server 2012 R2 にインストールされている KMS を更新する必要があります。 詳しくは、 [Windows 8.1 および Windows Server 2012 R2 の 2016 年 7 月の更新プログラムのロールアップ](https://support.microsoft.com/help/3172614/july-2016-update-rollup-for-windows-8.1-and-windows-server-2012-r2)に関するページをご覧ください。  
> - Windows Server 2008 R2 については、Windows Server 2016 またはそれ以降のオペレーティング システムを実行しているクライアントをライセンス認証できるようにする更新プログラムはありません。 

1 つの KMS ホストで無制限の数の KMS クライアントをサポートできます。 50 台を超えるクライアントがある場合は、KMS ホストが使用できなくなった場合に備えて 2 台以上の KMS ホストを用意することをお勧めします。 ほとんどの組織では、2 つの KMS ホストでインフラストラクチャ全体をサポートできます。

# <a name="addressing-kms-operational-requirements"></a>KMS の運用要件への対応
KMS は、物理コンピューターと仮想コンピューターをライセンス認証できます。しかし、KMS ライセンス認証を行うには、ネットワークに最小限の数 ("ライセンス認証のしきい値" といいます) のコンピューターが存在している必要があります。 このしきい値が満たされたうえで、KMS クライアントのライセンス認証を行うことができます。 ライセンス認証のしきい値が満たされていることを確認するために、KMS ホストは、ネットワーク上でライセンス認証を要求しているコンピューターの数を数えます。

KMS ホストは、最新の接続をカウントします。 クライアントまたはサーバーが KMS ホストにコンタクトすると、ホストはマシン ID をカウントに追加し、応答時に現在のカウント値を返します。 カウント数が十分であれば、クライアントまたはサーバーがライセンス認証されます。 クライアントは、カウントが 25 以上の場合にライセンス認証されます。 Microsoft Office 製品のサーバーおよびボリューム エディションは、カウントが 5 以上の場合にライセンス認証されます。 KMS は、過去 30 日間の一意の接続のみをカウントし、直近 50 件のコンタクトだけを保存します。

KMS ライセンス認証の有効期間は 180 日間です。これはライセンス認証の一般的な有効期間です。 KMS クライアントは、認証状態を維持するために、少なくとも 180 日ごとに 1 回 KMS ホストに接続してライセンス認証を更新する必要があります。 KMS クライアント コンピューターは、既定で 7 日ごとにライセンス認証を更新します。 クライアントのライセンス認証が更新された後、再びライセンス認証の有効期間が開始されます。

# <a name="addressing-kms-functional-requirements"></a>KMS の機能要件への対応

KMS ライセンス認証では、TCP/IP 接続が必要になります。 KMS ホストおよびクライアントは、既定でドメイン ネーム システム (DNS) を使用するように構成されます。 KMS ホストは、既定で DNS 動的更新を使用して、KMS クライアントが KMS ホストを検出して接続するために必要な情報を自動的に公開します。 これらの既定の設定をそのまま使用することもできますが、特殊なネットワークおよびセキュリティ構成要件がある場合は KMS ホストおよびクライアントを手動で構成することもできます。

最初の KMS ホストがライセンス認証された後、最初のホスト上で使用されている KMS キーを使用して、ネットワーク上の KMS ホストを 5 つまでライセンス認証できます。 KMS ホストがライセンス認証された後、管理者は、同じキーを使用して、同じホストに対してライセンスの再認証を 9 回まで行うことができます。

組織において 6 つを超える KMS ホストが必要な場合は、組織の KMS キーに対して追加のライセンス認証を申請する必要があります。たとえば、1 つのボリューム ライセンス認証契約に 10 か所の物理位置が含まれ、それぞれの位置にローカル KMS ホストを配置する場合などがこれに該当します。

> [!NOTE] 
> この例外を申請するには、ライセンス認証コール センターまでお問い合わせください。 詳細については、「 [マイクロソフト ボリューム ライセンス]( https://www.microsoft.com/licensing)」を参照してください。

Windows 10、Windows Server 2016、Windows 8.1、Windows Server 2012 R2、Windows Server 2012、Windows 7、Windows Server 2008 R2 のボリューム ライセンス版が実行されているコンピューターは、既定で、追加の構成が必要ない KMS クライアントとなります。

コンピューターを KMS ホスト、MAK、または製品版の KMS クライアントから変換する場合は、該当する KMS クライアント セットアップ キーをインストールしてください。 詳細については、 [KMS クライアント セットアップ キー](KMSclientkeys.md)に関するページを参照してください。 
