---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービスのテクニカル リファレンス
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 31c7c53a5dd28813076fcaa745093050808b5755
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405225"
---
# <a name="windows-time-service"></a>Windows タイム サービス

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降


**このガイドの手順**  
  
* Windows タイムサービスの構成情報の検索場所  
* Windows タイムサービスとは何ですか。  
* タイムプロトコルの重要性  
* Windows タイム サービスのしくみ   
* Windows タイム サービスのツールと設定  
  
> [!NOTE]  
> Windows Server 2003 および Microsoft Windows 2000 Server では、ディレクトリ サービスを Active Directory ディレクトリ サービスと呼びます。 Windows Server 2008 R2 および Windows Server 2008 では、ディレクトリサービスの名前は Active Directory Domain Services (AD DS) です。 このトピックの残りの部分では AD DS を参照しますが、この情報は Windows Server 2016 の Active Directory Domain Services にも適用されます。  
  
Windows タイムサービスは、W32Time とも呼ばれ、AD DS ドメイン内で実行されているすべてのコンピューターの日付と時刻を同期します。 時間の同期は、多くの Windows サービスと基幹業務アプリケーションを適切に操作するために不可欠です。 Windows タイムサービスはネットワークタイムプロトコル (NTP) を使用してネットワーク上のコンピューターの時計を同期します。これにより、正確なクロック値 (タイムスタンプ) をネットワーク検証およびリソースアクセス要求に割り当てることができます。 サービスは、NTP および time プロバイダーを統合することで、エンタープライズ管理者が信頼性の高いスケーラブルなタイムサービスを実現します。
  
> [!IMPORTANT]  
> Windows Server 2016 より前では、W32Time サービスは、時間の影響を受けるアプリケーションのニーズを満たすように設計されていませんでした。  ただし、Windows Server 2016 の更新プログラムにより、ドメインに1ミリ秒の精度を実現するためのソリューションを実装できるようになりました。  詳細については、「 [windows 2016 の正確な時刻](accurate-time.md)とサポートの境界」を参照して[、高精度の環境用に windows タイムサービスを構成](support-boundary.md)してください。  
  
## <a name="BKMK_Config"></a>Windows タイムサービスの構成情報の検索場所  
このガイドでは、Windows タイムサービスの構成については説明し**ません**。 Windows タイムサービスを構成する手順について説明している、Microsoft TechNet と Microsoft サポート技術情報のさまざまなトピックがあります。 構成情報が必要な場合は、次のトピックを参考にして、適切な情報を見つけることができます。  
  
-   フォレストルートプライマリドメインコントローラー (PDC) エミュレーターの Windows タイムサービスを構成するには、次を参照してください。  
  
    -   [フォレストルートドメインの PDC エミュレーターで Windows タイムサービスを構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [フォレストのタイムソースの構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Windows server 2008 R2、Windows Server 2008、Windows Server 2003、および Windows を実行しているコンピューターの構成設定について説明しているマイクロソフトサポート技術情報の記事816042、 [Windows server で権限のあるタイムサーバーを構成する方法](https://go.microsoft.com/fwlink/?LinkID=60402)について説明します。サーバー 2003 R2。  
  
-   任意のドメインメンバークライアントまたはサーバー、またはフォレストルート PDC エミュレーターとして構成されていないドメインコントローラーで Windows タイムサービスを構成するには、「[ドメイン時刻の自動同期を行うようにクライアントコンピューターを構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)する」を参照してください。  
  
    > [!WARNING]  
    > アプリケーションによっては、コンピューターに高精度のタイムサービスが必要になる場合があります。 その場合は、手動のタイムソースを構成することもできますが、Windows タイムサービスは正確なタイムソースとして機能するように設計されていないことに注意してください。 Microsoft サポート技術情報の記事939322で説明されているように、高精度の時間環境のサポート制限を認識していることを確認します。また、[高精度の環境では、Windows タイムサービスを構成する](support-boundary.md)ための境界をサポートします。  
  
-   ドメインメンバーではなく、ワークグループメンバーとして構成されている Windows ベースのクライアントコンピューターまたはサーバーコンピューターで Windows タイムサービスを構成するには、「[選択したクライアントコンピューターの手動のタイムソースを構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)する」を参照してください。  
  
-   仮想環境を実行するホストコンピューターで Windows タイムサービスを構成する方法については、マイクロソフトサポート技術情報の記事816042「 [Windows server で権限のあるタイムサーバーを構成する方法](https://go.microsoft.com/fwlink/?LinkID=60402)」を参照してください。 マイクロソフト以外の仮想化製品を使用している場合は、その製品の製造元のドキュメントを参照してください。  
  
-   仮想マシンで実行されているドメインコントローラーで Windows タイムサービスを構成するには、ドメインコントローラーとして動作するホストシステムとゲストオペレーティングシステム間の時間の同期を部分的に無効にすることをお勧めします。 これにより、ゲストドメインコントローラーはドメイン階層の時間を同期させることができますが、保存された状態から復元された場合は、時間のずれを防ぐことができます。 詳細については、Microsoft サポート技術情報の記事976924を参照してください。 windows[タイムサービスイベント id 24、29、および38は、hyper-v と展開を使用する Windows Server 2008 ベースのホストサーバーで実行されている仮想化ドメインコントローラーで受信し](https://go.microsoft.com/fwlink/?LinkID=192236)ます。 [仮想化ドメインコントローラーに関する考慮事項](https://go.microsoft.com/fwlink/?LinkID=192235)  
  
-   仮想コンピューターでも実行されているフォレストルート PDC エミュレーターとして機能するドメインコントローラーで Windows タイムサービスを構成するには、「 [PDC での Windows タイムサービスの構成」の説明に従って、物理コンピューターについて同じ手順を実行します。フォレストルートドメイン内のエミュレーター](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)。  
  
-   仮想コンピューターとして実行されているメンバーサーバーで Windows タイムサービスを構成するには、「」の説明に従って、ドメイン時間の階層を使用します (「[ドメイン時刻の自動同期を行うようにクライアントコンピューターを構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)する」を参照)。  
  
## <a name="BKMK_WTS"></a>Windows タイムサービスとは何ですか。  
Windows タイムサービス (W32Time) は、広範な構成を必要としないコンピューターのネットワーククロック同期を提供します。  
  
Windows タイムサービスは、Kerberos バージョン5認証を正常に動作させるために不可欠であり、したがって AD DS ベースの認証にも対応しています。 ほとんどのセキュリティサービスを含むすべての Kerberos 対応アプリケーションは、認証要求に参加しているコンピューター間の時間の同期に依存します。 また AD DS ドメインコントローラーには、正確なデータレプリケーションを確実に行うために、同期されたクロックが必要です。  
  
Windows タイムサービスは、W32Time というダイナミックリンクライブラリに実装されています。 既定では、オペレーティングシステムのセットアップおよびインストール中**に、W32Time**は既定でインストールされます。  
  
W32Time は、Kerberos V5 認証プロトコルによる仕様をサポートするために、当初は Windows 2000 Server 向けに開発されたもので、ネットワーク上でクロックを同期する必要がありました。 Windows Server 2003 以降では、Windows 2000 サーバーオペレーティングシステムでのネットワーククロック同期の精度が向上しました。さらに、さまざまなハードウェアデバイスとネットワークタイムプロトコルを時間によってサポートするようになりました。プロバイダー. もともと Kerberos 認証用にクロック同期を提供するように設計されていましたが、現在のアプリケーションの多くは、タイムスタンプを使用してトランザクションの一貫性を確保し、重要なイベントの時間と、その他のビジネスクリティカルな時間を記録します。参照. これらのアプリケーションは、Windows タイムサービスによって提供されるコンピューター間の時間の同期の恩恵を受けます。  
  
## <a name="BKMK_TimeProtocols"></a>タイムプロトコルの重要性  
時刻のプロトコルは、時刻情報を交換するために2台のコンピューター間で通信し、その情報を使用してクロックを同期します。 Windows タイムサービス時間プロトコルでは、クライアントはサーバーから時刻情報を要求し、受信した情報に基づいてクロックを同期します。  
  
Windows タイムサービスは、NTP を使用してネットワーク経由で時間を同期します。 NTP は、時計を同期させるために必要な作業分野のアルゴリズムを含むインターネット時刻プロトコルです。 NTP は、Windows の一部のバージョンで使用される Simple Network Time Protocol (SNTP) よりも正確なタイムプロトコルです。ただし、W32Time は引き続き SNTP をサポートして、Windows 2000 などの SNTP ベースのタイムサービスを実行しているコンピューターとの下位互換性を確保します。  
  
## <a name="see-also"></a>関連項目  
[Windows タイムサービスのしくみ](How-the-Windows-Time-Service-Works.md)  
[Windows タイム サービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)  
[マイクロソフトサポート技術情報の記事902229](https://go.microsoft.com/fwlink/?LinkId=186066)