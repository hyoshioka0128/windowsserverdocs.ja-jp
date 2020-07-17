---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービスのテクニカル リファレンス
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 51711d423582aee4ebc3762a51abe9156754b55a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860135"
---
# <a name="windows-time-service"></a>Windows タイム サービス

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降


**このガイドの内容**  
  
* Windows タイム サービスの構成情報を検索する場所  
* Windows タイム サービスとは  
* タイム プロトコルの重要性  
* Windows タイム サービスのしくみ   
* Windows タイム サービスのツールと設定  
  
> [!NOTE]  
> Windows Server 2003 および Microsoft Windows 2000 Server では、ディレクトリ サービスを Active Directory ディレクトリ サービスと呼びます。 Windows Server 2008 R2 および Windows Server 2008 では、ディレクトリ サービスは Active Directory Domain Services (AD DS) と呼びます。 このトピックの以降の部分では、AD DS について取り上げますが、その情報は Windows Server 2016 の Active Directory Domain Services にも適用できます。  
  
Windows タイム サービス (W32Time とも呼ばれます) は、AD DS ドメイン内で実行されているすべてのコンピューターの日付と時刻を同期します。 多くの Windows サービスと基幹業務アプリケーションを適切に操作するためには、時間の同期は不可欠です。 Windows タイム サービスはネットワーク タイム プロトコル (NTP) を使用してネットワーク上のコンピューターのクロックを同期します。これにより、正確なクロック値 (タイム スタンプ) をネットワーク検証およびリソース アクセス要求に割り当てることができます。 サービスでは NTP とタイム プロバイダーを統合して、エンタープライズ管理者にとって信頼性の高いスケーラブルなタイム サービスを実現します。
  
> [!IMPORTANT]  
> Windows Server 2016 より前では、W32Time サービスは、厳密な時間管理を要するアプリケーションのニーズを満たすように設計されていませんでした。  しかし、Windows Server 2016 の更新プログラムによって、1 ミリ秒の精度のソリューションをドメインに実装できるようになりました。  詳細については、[Windows 2016 の正確な時刻](accurate-time.md)および[高精度の環境向けに Windows タイム サービスを構成するためのサポート範囲](support-boundary.md)に関する記事を参照してください。  
  
## <a name="where-to-find-windows-time-service-configuration-information"></a><a name="BKMK_Config"></a>Windows タイム サービスの構成情報を検索する場所  
このガイドでは、Windows タイムサービスの構成については**説明していません**。 Windows タイム サービスを構成する手順について説明している各種のトピックは、Microsoft TechNet 上や Microsoft サポート技術情報にあります。 構成情報が必要な場合は、次のトピックを参考にすると、適切な情報を見つけることができます。  
  
-   フォレスト ルート プライマリ ドメイン コントローラー (PDC) エミュレーター向けに Windows タイム サービスを構成するには、次を参照してください。  
  
    -   [フォレスト ルート ドメインの PDC エミュレーター上で Windows タイム サービスを構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [フォレストにタイム ソースを構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   Microsoft サポート技術情報の記事 816042「[Windows Server で権限のあるタイム サーバーを構成する方法](https://go.microsoft.com/fwlink/?LinkID=60402)」では、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003、Windows Server 2003 R2 を実行するコンピューターの構成設定について説明されています。  
  
-   任意のドメイン メンバー クライアントまたはサーバー上に、あるいは、フォレスト ルート PDC エミュレーターとして構成されていないドメイン コントローラー上であっても、Windows タイム サービスを構成するには、「[ドメイン時刻の自動同期のためにクライアント コンピューターを構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)」を参照してください。  
  
    > [!WARNING]  
    > アプリケーションによっては、コンピューターに高精度のタイム サービスが必要になる場合があります。 その場合は、手動のタイム ソースを構成することもできますが、Windows タイム サービスは高精度なタイム ソースとして機能するように設計されていなかったことに注意してください。 [高精度の環境に Windows タイム サービスを構成する場合のサポート範囲](support-boundary.md)に関して示した Microsoft サポート技術情報の記事 939322 に説明されているように、必ず高精度な時間の環境に対するサポートの制限事項に注意してください。  
  
-   ドメイン メンバーではなくワークグループ メンバーとして構成された Windows ベースのクライアントまたはサーバー コンピューター上に Windows タイム サービスを構成するには、「[選択されたクライアント コンピューターに手動のタイム ソースを構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)」を参照してください。  
  
-   仮想環境を実行するホスト コンピューター上に Windows タイム サービスを構成するには、Microsoft サポート技術情報の記事 816042「[Windows Server で権限のあるタイム サーバーを構成する方法](https://go.microsoft.com/fwlink/?LinkID=60402)」を参照してください。 Microsoft 以外の仮想化製品を利用している場合は、必ずその製品のベンダーのドキュメントを参照してください。  
  
-   仮想マシンで実行されているドメイン コントローラー上に Windows タイム サービスを構成するには、ドメイン コントローラーとして動作するホスト システムとゲスト オペレーティング システム間での時間の同期を、一部無効にすることをお勧めします。 これにより、ゲスト ドメイン コントローラーではドメイン階層用に時間を同期できますが、保存済み状態から復元される際に、時間のずれを防ぐことができます。 詳細については、Microsoft サポート技術情報の記事 976924 「[ Hyper-V を利用した Windows Server 2008 ベース ホスト サーバー上で実行されている仮想化ドメイン コントローラーで、Windows タイム サービス イベント ID 24、29、38 を受信する](https://go.microsoft.com/fwlink/?LinkID=192236)」と、[仮想化ドメイン コントローラーの展開時の考慮事項](https://go.microsoft.com/fwlink/?LinkID=192235)に関する記事を参照してください。  
  
-   仮想コンピューターでも実行されるフォレスト ルート PDC エミュレーターとして動作するドメイン コントローラー上に、Windows タイム サービスを構成するには、[フォレスト ルート ドメインの PDC エミュレーター上での Windows タイム サービスの構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)に関する記事に説明されているように、物理コンピューターの場合と同じ手順に従ってください。  
  
-   仮想コンピューターとして実行されているメンバー サーバー上に Windows タイム サービスを構成するには、「[クライアント コンピューターにドメイン時間の自動同期を構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)」に説明されているように、ドメイン時間の階層を使用してください。  
  
## <a name="what-is-the-windows-time-service"></a><a name="BKMK_WTS"></a>Windows タイム サービスとは  
Windows タイム サービス (W32Time) を使用すると、広範な構成を必要とせずに、コンピューターのネットワーク クロックの同期を行うことができます。  
  
Kerberos バージョン 5 認証が正常に動作するには、Windows タイム サービスは必須であり、必然的に AD DS ベースの認証にとっても必須です。 ほとんどのセキュリティ サービスを含む Kerberos 対応アプリケーションでは、認証要求に参加しているコンピューター間で時間が同期されていることを前提としています。 また、AD DS ドメイン コントローラーでは、正確なデータ レプリケーションを保証できるように、クロックが同期している必要があります。  
  
Windows タイム サービスは、W32Time.dll という動的リンク ライブラリに実装されています。 W32Time.dll は既定で、オペレーティング システムのセットアップとインストールの際に、 **%Systemroot%\System32** フォルダー内にインストールされます。  
  
W32Time.dll は、ネットワーク上でクロックを同期する必要がある Kerberos V5 認証プロトコルによる仕様をサポートするために、当初は Windows 2000 Server 向けに開発されました。 Windows Server 2003 以降、W32Time.dll では、Windows 2000 Server オペレーティング システムでのネットワーク クロック同期の精度を向上させ、タイム プロバイダーの手法によってさまざまなハードウェア デバイスおよびネットワーク タイム プロトコルがサポートされました。 当初は Kerberos 認証用にクロック同期を提供するように設計されていましたが、現在の多くのアプリケーションでは、タイムスタンプを使用してトランザクションの一貫性が確保され、重要なイベントの時間やその他の厳密な時間管理を要するビジネスクリティカルな情報が記録されます。 Windows タイム サービスによって提供されるコンピューター間での時間の同期は、これらのアプリケーションにとって有益です。  
  
## <a name="importance-of-time-protocols"></a><a name="BKMK_TimeProtocols"></a>タイム プロトコルの重要性  
タイム プロトコルでは、2 つのコンピューター間で通信して時間情報をやり取りし、その情報を使ってクロックを同期します。 Windows タイム サービスのタイム プロトコルを利用すると、クライアントではサーバーからの時間情報が要求され、受信された情報に基づいてそのクロックが同期されます。  
  
Windows タイム サービスでは NTP を使用して、ネットワーク経由で時間を同期できます。 NTP は、時計を同期させるために必要な作業分野のアルゴリズムを含むインターネット時刻プロトコルです。 NTP は、Windows の一部のバージョンで使用される簡易ネットワーク タイム プロトコル (SNTP) よりも正確なタイム プロトコルです。ただし、W32Time では引き続き SNTP をサポートして、Windows 2000 などの SNTP ベースのタイム サービスを実行しているコンピューターとの下位互換を可能にしています。  
  
## <a name="see-also"></a>参照  
[Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)  
[Windows タイム サービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft サポート技術情報の記事 902229](https://go.microsoft.com/fwlink/?LinkId=186066)