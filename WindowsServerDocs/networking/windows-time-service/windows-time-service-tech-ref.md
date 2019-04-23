---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービスのテクニカル リファレンス
description: W32Time サービスは、ネットワークの広範な構成を必要としないコンピューターのクロックの同期を提供します。 W32Time サービスは、重要なは、Kerberos V5 認証の成功した操作と、そのためは AD DS ベースの認証です。
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 904a53797d22d2e06e0cd2f7572b99fc386dae16
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845123"
---
# <a name="windows-time-service-technical-reference"></a>Windows タイム サービスのテクニカル リファレンス
>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降

W32Time サービスは、ネットワークの広範な構成を必要としないコンピューターのクロックの同期を提供します。 W32Time サービスは、重要なは、Kerberos V5 認証の成功した操作と、そのためは AD DS ベースの認証です。 ほとんどのセキュリティ サービスを含む、任意の Kerberos 対応アプリケーションは、認証要求に参加しているコンピューター間の時刻同期に依存します。 AD DS ドメイン コント ローラーも正確なデータのレプリケーションを確認するに役立ちますクロックを同期している必要があります。

> [!NOTE]  
> Windows Server 2003 および Microsoft Windows 2000 Server では、ディレクトリ サービスを Active Directory ディレクトリ サービスと呼びます。 Windows Server 2008 R2 および Windows Server 2008 では、ディレクトリ サービスを Active Directory Domain Services (AD DS) と呼びます。 このトピックの残りの部分を指す、AD DS が、情報は、Windows Server 2016 での Active Directory Domain Services に適用できます。

W32Time サービスは W32Time.dll で、既定でインストールされていると呼ばれるダイナミック リンク ライブラリで実装された **%Systemroot%\System32**します。 W32Time.dll は、クロックを同期できるネットワーク上に必要な Kerberos V5 認証プロトコルによってもともと仕様をサポートするために Windows 2000 Server の開発されました。 W32Time.dll 以降 Windows Server 2003 では、Windows Server 2000 オペレーティング システムをネットワークの時計の同期の精度向上を用意されています。 さらに、Windows Server 2003、W32Time.dll には、さまざまなハードウェア デバイスとタイム プロバイダーを使用して、ネットワーク タイム プロトコルがサポートされています。

現在の多くのアプリケーションが、トランザクションの一貫性との重要なイベント、およびその他のビジネスに不可欠な時間を記録するタイムスタンプを使用して Kerberos 認証用の時計の同期を提供するもともと設計されていますが、時間を区別します。情報。  これらのアプリケーション、Windows タイム サービスによって提供されるコンピューター間の時刻同期を享受できます。

## <a name="importance-of-time-protocols"></a>時間プロトコルの重要性
時間プロトコルは、時間の情報を交換し、その情報を使用して、クロックの同期を 2 台のコンピューター間で通信します。 Windows タイム サービス時間プロトコルでは、クライアントは、サーバーから時刻の情報を要求し、受信する情報に基づいて、そのクロックを同期します。
  
Windows タイム サービスは、NTP を使用して、ネットワーク経由で時刻を同期します。 NTP は、時計を同期させるために必要な作業分野のアルゴリズムを含むインターネット時刻プロトコルです。 NTP がより正確なタイム プロトコルよりも、単純なネットワーク タイム プロトコル (SNTP) Windows; の一部のバージョンで使用されています。ただし、W32Time は、Windows 2000 などの SNTP ベースのタイム サービスを実行しているコンピューターとの下位互換性を有効にする SNTP をサポートするためには続行されます。
<!-- maybe this should be its own topic under the Tech Ref section -->
## <a name="where-to-find-windows-time-service-configuration-related-information"></a>Windows タイム サービスの構成に関する情報の入手先  
このガイドは**いない**Windows タイム サービスの構成について説明します。 いくつか異なるトピックは Microsoft technet、マイクロソフト サポート技術情報では、Windows タイム サービスを構成する手順を説明します。 構成情報を必要とする場合、次のトピックは、適切な情報を見つけるに役立ちます。  
<!-- should this be an if/then table -->
-   フォレストのルート プライマリ ドメイン コント ローラー (PDC) エミュレーターの Windows タイム サービスを構成するを参照してください。  
  
    -   [フォレスト ルート ドメインの PDC エミュレーターで Windows タイム サービスを構成します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [フォレストのタイム ソースを構成します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   マイクロソフト サポート技術情報記事 816042、 [Windows Server で、権限のあるタイム サーバーを構成する方法](https://go.microsoft.com/fwlink/?LinkID=60402)、Windows Server 2008 R2、Windows Server 2008、Windows Server を実行しているコンピューターの構成設定の説明2003、および Windows Server 2003 R2。  
  
-   ドメイン メンバー クライアントまたはサーバー、または偶数のドメイン コント ローラーをフォレスト ルート PDC エミュレーターとして構成されていない、Windows タイム サービスを構成するを参照してください[自動ドメインの時刻の同期用のクライアントコンピューターを構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
    > [!WARNING]  
    > 一部のアプリケーションでは、正確度の高いタイム サービスが自分のコンピューターを必要があります。 ケースがある場合は、手動のタイム ソースでは、構成しますが、Windows タイム サービスを関数の正確なタイム ソースとして設計されていませんすることができます。 把握するには、サポートの制限の正確度の高い環境では、マイクロソフト サポート技術情報の説明に従って記事 939322 のことを確認[高精度環境Windowsタイムサービスを構成するサポート境界](support-boundary.md).  
  
-   Windows ベース コンピューター上でクライアントまたはサーバーのドメインのメンバーではなくワークグループのメンバーのように構成されている、Windows タイム サービスを構成する[選択したクライアント コンピューターの手動のタイム ソースを構成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29)します。  
  
-   仮想環境を実行しているホスト コンピューターで Windows タイム サービスを構成するには、マイクロソフト サポート技術情報記事 816042 を参照してください[Windows Server で、権限のあるタイム サーバーを構成する方法](https://go.microsoft.com/fwlink/?LinkID=60402)します。 Microsoft 以外の仮想化製品を使用する場合は、その製品のベンダーのドキュメントを参照してください、します。  
  
-   仮想マシンで実行されているドメイン コント ローラーで、Windows タイム サービスを構成するには、ドメイン コント ローラーとして機能するホスト システムとゲスト オペレーティング システム間の時刻同期を部分的に無効にすることをお勧めします。 これにより、時間の同期ドメインの階層用に、ゲストのドメイン コント ローラーが、時刻のずれの場合、これが保存された状態から復元されたことから保護します。 詳細については、マイクロソフト サポート技術情報記事 976924 を参照してください[、Hyper-v と Windows Server 2008 ベースのホスト サーバーで実行されている仮想化ドメイン コント ローラー上の Windows タイム サービス イベント Id 24、29、および 38 を受信する](https://go.microsoft.com/fwlink/?LinkID=192236)。[仮想化ドメイン コント ローラーの展開に関する考慮事項](https://go.microsoft.com/fwlink/?LinkID=192235)します。  
  
-   仮想コンピューターで実行されても、フォレスト ルート PDC エミュレーター役割を果たすドメイン コント ローラー上で、Windows タイム サービスを構成する手順は同じ物理コンピューターについて」の説明に従って[で、Windows タイム サービスを構成します。フォレスト ルート ドメインの PDC エミュレーター](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)します。  
  
-   仮想コンピューターとして実行されているメンバー サーバー上で、Windows タイム サービスを構成するにはドメインの時間階層を」の説明に従って使用[自動ドメイン時刻の同期用のクライアント コンピューターを構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29)します。


> [!IMPORTANT]  
> Windows Server 2016 では、前に、W32Time サービスが時間を区別するアプリケーションのニーズを満たす設計されていません。  ただし、Windows Server 2016 に更新できるようになりました 1 ミリ秒のソリューションを実装するドメインで精度。  詳細については、次を参照してください。 [Windows 2016 の正確性時間](accurate-time.md)と[高精度の環境の Windows タイム サービスを構成するサポート境界](support-boundary.md)詳細についてはします。

## <a name="related-topics"></a>関連トピック
- [Windows 2016 の正確な時刻](accurate-time.md)
- [Windows Server 2016 の時間精度の向上](windows-server-2016-improvements.md)  
- [Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)  
- [Windows タイム サービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)  
- [高精度の環境の Windows タイム サービスを構成するサポート境界](support-boundary.md)
- [マイクロソフト サポート技術情報の記事 902229](https://go.microsoft.com/fwlink/?LinkId=186066)