---
title: SMBv1 は、Windows 10 バージョン1709、Windows Server バージョン1709以降のバージョンでは既定でインストールされません。
description: Windows 10 の SMBv1 プロトコルの動作について説明します。この更新プログラムと Windows Server バージョン1709以降のバージョンが含まれます。
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: fdc90c6e5d6790348fafc12079eec5ac7e387b3f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815315"
---
# <a name="smbv1-is-not-installed-by-default-in-windows-10-version-1709-windows-server-version-1709-and-later-versions"></a>SMBv1 は、Windows 10 バージョン1709、Windows Server バージョン1709以降のバージョンでは既定でインストールされません。

## <a name="summary"></a>要約

Windows 10 秋の更新プログラムおよび Windows Server バージョン 1709 (RS3) 以降のバージョンでは、Server Message Block version 1 (SMBv1) のネットワークプロトコルは既定でインストールされなくなりました。 2007年以降、SMBv2 以降のプロトコルに置き換えられました。 Microsoft は、2014の SMBv1 プロトコルを一般に非推奨としました。 

SMBv1 では、Windows 10 秋の更新プログラムおよび Windows Server バージョン 1709 (RS3) で次の動作が実行されます。 
 
- SMBv1 には、個別にアンインストールできるクライアントとサーバーの両方のサブ機能が用意されました。    
- Windows 10 Enterprise および Windows 10 の教育には、クリーンインストール後に既定で SMBv1 クライアントまたはサーバーが含まれなくなりました。    
- Windows Server 2016 には、クリーンインストール後に既定で SMBv1 クライアントまたはサーバーが含まれなくなりました。    
- Windows 10 Home と Windows 10 Professional では、クリーンインストール後に既定で SMBv1 サーバーが含まれなくなりました。    
- Windows 10 Home と Windows 10 Professional には、クリーンインストール後も既定で SMBv1 クライアントが含まれています。 SMBv1 クライアントが合計で15日間使用されていない場合 (オフになっているコンピューターは除く)、自動的に自動的にアンインストールされます。    
- Windows 10 Home と Windows 10 Professional のインプレースアップグレードと Insider 便では、最初に SMBv1 が自動的に削除されるわけではありません。 SMBv1 クライアントまたはサーバーが合計で15日間使用されていない (コンピューターがオフになっている時間を除く) 場合、それぞれが自動的にアンインストールされます。     
- Windows 10 Enterprise および Windows 10 教育エディションのインプレースアップグレードと Insider 便では、SMBv1 は自動的には削除されません。 管理者は、これらの管理された環境で SMBv1 をアンインストールすることを決定する必要があります。 Windows 10 バージョン 1809 (RS5) 以降のバージョンでは、管理者は "SMB 1.0/CIFS 自動削除" 機能を有効にすることで、SMBv1 の自動削除を有効にすることができます。    
- 15日後の SMBv1 の自動削除は、1回限りの操作です。 管理者が SMBv1 を再インストールした場合、それ以上のアンインストールは試行されません。
- SMB バージョン2.02、2.1、3.0、3.02、および3.1.1 の各機能はまだ完全にサポートされており、SMBv2 バイナリの一部として既定で含まれています。    
- Computer Browser サービスは SMBv1 に依存しているため、SMBv1 クライアントまたはサーバーがアンインストールされると、サービスはアンインストールされます。 これは、従来の NetBIOS データグラムブラウズ方法を使用して、エクスプローラー Networkcan Windows コンピューターを表示できなくなることを意味します。    
- SMBv1 は、Windows 10 および Windows Server 2016 のすべてのエディションでも再インストールできます。    
 
  > [!NOTE]
  > Windows 10、バージョン 1803 (RS4) Professional は、Windows 10、バージョン 1703 (RS2)、Windows 10、バージョン 1607 (RS1) と同じ方法で SMBv1 を処理します。 この問題は、Windows 10 バージョン 1809 (RS5) で修正されました。 SMBv1 は、手動でアンインストールすることもできます。 ただし、次のシナリオでは、Windows は15日後に SMBv1 を自動的にアンインストールしません。 
 
-  Windows 10 バージョン1803のクリーンインストールを実行します。     
-  Windows 10、バージョン1607、または Windows 10、バージョン1703を windows 10、バージョン1803に直接アップグレードする場合は、最初に Windows 10 バージョン1709にアップグレードする必要があります。     
 
SMBv1 のみをサポートしているデバイスに接続しようとした場合、またはこれらのデバイスが接続を試みた場合は、次のエラーメッセージのいずれかが表示されることがあります。     

```
You can't connect to the file share because it's not secure. This share requires the obsolete SMB1 protocol, which is unsafe and could expose your system to attack.
Your system requires SMB2 or higher. For more info on resolving this issue, see: https://go.microsoft.com/fwlink/?linkid=852747  
```

```
The specified network name is no longer available.
```

```
Unspecified error 0x80004005
```

```
System Error 64
```

```
The specified server cannot perform the requested operation.
```

```
Error 58
```    

次のイベントは、リモートサーバーがこのクライアントからの SMBv1 接続を必要としていますが、SMBv1 がアンインストールされているか、クライアントで無効になっている場合に表示されます。

```
Log Name:      Microsoft-Windows-SmbClient/Security
 Source:        Microsoft-Windows-SMBClient
 Date:          Date/Time
 Event ID:      32002
 Task Category: None
 Level:         Info
 Keywords:      (128)
 User:          NETWORK SERVICE
 Computer:      junkle.contoso.com
 Description:
 The local computer received an SMB1 negotiate response. 

Dialect: 
SecurityMode 
Server name: 

Guidance: 
SMB1 is deprecated and should not be installed nor enabled. For more information, see https://go.microsoft.com/fwlink/?linkid=852747.
```

```
Log Name:      Microsoft-Windows-SmbClient/Security
 Source:        Microsoft-Windows-SMBClient
 Date:          Date/Time
 Event ID:      32000
 Task Category: None
 Level:         Info
 Keywords:      (128)
 User:          NETWORK SERVICE
 Computer:      junkle.contoso.com
 Description: 
SMB1 negotiate response received from remote device when SMB1 cannot be negotiated by the local computer. 
Dialect: 
Server name: 

Guidance: 
The client has SMB1 disabled or uninstalled. For more information: https://go.microsoft.com/fwlink/?linkid=852747.     
```

これらのデバイスは、Windows を実行している可能性があります。 SMB サービスを提供するために、以前のバージョンの Linux や Samba などのサードパーティ製ソフトウェアが実行されている可能性が高くなります。 多くの場合、これらのバージョンの Linux および Samba はサポートされなくなりました。 

> [!NOTE]
> Windows 10 バージョン1709は、"作成者の更新" とも呼ばれます。   

## <a name="more-information"></a>詳細

この問題を回避するには、SMBv1 のみをサポートしている製品の製造元に連絡し、SMBv 2.02 以降のバージョンをサポートするソフトウェアまたはファームウェアの更新プログラムを要求します。 既知のベンダーとその SMBv1 の要件の最新の一覧については、次の Windows および Windows Server Storage エンジニアリングチームのブログ記事を参照してください。 

[SMBv1 製品クリアリングハウス](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/SMB1-Product-Clearinghouse/ba-p/426008) 
#### <a name="leasing-mode"></a>リースモード

Oplock を無効にする必要があるなど、レガシソフトウェアの動作に対してアプリケーションの互換性を提供するために SMBv1 が必要な場合、Windows はリースモードと呼ばれる新しい SMB 共有フラグを提供します。このフラグは、リースや oplock などの最新の SMB セマンティクスを共有が無効にするかどうかを指定します。

Oplock またはリースを使用せずに共有を指定して、レガシアプリケーションが SMBv2 以降のバージョンで動作できるようにすることができます。 これを行うには、 **-LeasingMode None** パラメーターと共に**New-smbshare**または**new-smbshare** PowerShell コマンドレットを使用します。

> [!NOTE]
> このオプションは、サードパーティ製のアプリケーションが必要であることがわかっている場合に、レガシサポートに必要な共有に対してのみ使用してください。 スケールアウトファイルサーバーで使用されるユーザーデータ共有または CA 共有にリースモードを指定しないでください。 これは、oplock とリースを削除すると、ほとんどのアプリケーションで不安定性とデータ破損が発生するためです。 リースモードは、共有モードでのみ機能します。 任意のクライアントオペレーティングシステムで使用できます。

#### <a name="explorer-network-browsing"></a>エクスプローラーネットワークの参照

Computer Browser サービスは、SMBv1 プロトコルを利用して、Windows Explorer ネットワークノード ("ネットワークコンピューター" とも呼ばれます) を設定します。 このレガシプロトコルは、非推奨であり、ルーティングされず、セキュリティが制限されています。 サービスは SMBv1 なしでは機能できないため、同時に削除されます。

ただし、Windows ベースのコンピューターを検索するために、ネットワーク受信ホームと小規模のビジネスワークグループ環境を使用する必要がある場合は、SMBv1 を使用しなくなった Windows ベースのコンピューターで次の手順を実行できます。 
 
1. "Function Discovery Provider Host" および "Function Discovery Resource Publication" サービスを開始し、 **[自動 (遅延開始)]** に設定します。

2. エクスプローラーの [ネットワーク] を開くと、メッセージが表示されたらネットワーク探索を有効にします。    
 
これらの設定を持つサブネット内のすべての Windows デバイスが、参照用にネットワークに表示されるようになります。 これは、WS-ADDRESSING プロトコルを使用します。 Windows デバイスが表示された後も、この参照リストにデバイスが表示されない場合は、他のベンダーや製造元にお問い合わせください。 このプロトコルが無効になっているか、SMBv1 のみがサポートされている可能性があります。

> [!NOTE]
> この機能を有効にするのではなく、ドライブとプリンターをマップすることをお勧めします。その場合でも、デバイスを検索して参照する必要があります。 マップされたリソースは見つけやすく、必要なトレーニングが少なく、使用する方が安全です。 これは、これらのリソースがグループポリシーによって自動的に提供される場合に特に当てはまります。 管理者は、IP アドレス、Active Directory Domain Services (AD DS)、Bonjour、Mdn、uPnP などを使用して、レガシコンピューターブラウザーサービス以外の方法で場所のプリンターを構成できます。

これらの回避策を使用できない場合、またはアプリケーションの製造元がサポートされているバージョンの SMB を提供できない場合は、「 [Windows の SMBv1、SMBv2、および SMBv3 を検出、有効化、および無効化する方法](detect-enable-and-disable-smbv1-v2-v3.md)」の手順に従って、手動で SMBv1 を再度有効にすることができます。

> [!IMPORTANT]
> SMBv1 を再インストールしないことを強くお勧めします。 これは、この古いプロトコルには、ランサムウェアやその他のマルウェアに関する既知のセキュリティ問題があるためです。  

#### <a name="windows-server-best-practices-analyzer-messaging"></a>Windows Server ベストプラクティスアナライザーメッセージング

Windows Server 2012 以降のサーバー操作システムには、ファイルサーバー用のベストプラクティスアナライザー (BPA) が含まれています。 SMB1 をアンインストールするための正しいオンラインガイダンスに従っている場合、この BPA を実行すると、矛盾した警告メッセージが返されます。

    Title: The SMB 1.0 file sharing protocol should be enabled
    Severity: Warning
    Date: 3/25/2020 12:38:47 PM
    Category: Configuration
    Problem: The Server Message Block 1.0 (SMB 1.0) file sharing protocol is disabled on this file server.
    Impact: SMB not in a default configuration, which could lead to less than optimal behavior.
    Resolution: Use Registry Editor to enable the SMB 1.0 protocol.

この特定の BPA 規則のガイダンスは無視してください。非推奨とされます。 繰り返し: SMB 1.0 を有効にしないでください。

## <a name="references"></a>参照

[SMB1 の使用を停止する](https://aka.ms/stopusingsmb1)
