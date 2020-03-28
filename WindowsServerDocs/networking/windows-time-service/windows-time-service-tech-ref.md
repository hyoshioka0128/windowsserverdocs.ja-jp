---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Windows タイム サービスのテクニカル リファレンス
description: W32Time サービスを使用すると、広範な構成を必要とせずに、コンピューターのネットワーク クロック同期を行うことができます。 W32Time サービスは Kerberos V5 認証が正常に動作するために必須の機能であるため、AD DS ベースの認証にも必須です。
author: eross-msft
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b3d66f47bea99f6eed55aac15f2b54f3401a5755
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314912"
---
# <a name="windows-time-service-technical-reference"></a>Windows タイム サービスのテクニカル リファレンス
>適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 10 以降

W32Time サービスを使用すると、広範な構成を必要とせずに、コンピューターのネットワーク クロック同期を行うことができます。 W32Time サービスは Kerberos V5 認証が正常に動作するために必須の機能であるため、AD DS ベースの認証にも必須です。 ほとんどのセキュリティ サービスを含む Kerberos 対応アプリケーションは、認証要求に参加しているコンピューター間で時間が同期されていることを前提としています。 AD DS ドメイン コントローラーでは、データ レプリケーションの正確を期すためにもクロックが同期している必要があります。

> [!NOTE]  
> Windows Server 2003 および Microsoft Windows 2000 Server では、ディレクトリ サービスを Active Directory ディレクトリ サービスと呼びます。 Windows Server 2008 R2 および Windows Server 2008 では、ディレクトリ サービスは Active Directory Domain Services (AD DS) と呼びます。 このトピックの残りの部分では、AD DS について取り上げますが、その情報は Windows Server 2016 の Active Directory Domain Services にも適用できます。

W32Time サービスは、既定で **%Systemroot%\System32** にインストールされる、W32Time.dll というダイナミック リンク ライブラリに実装されています。 W32Time.dll は、ネットワーク上でクロックを同期する必要がある Kerberos V5 認証プロトコルによる仕様をサポートするために、当初は Windows 2000 Server 向けに開発されたものでした。 Windows Server 2003 以降では、W32Time.dll により Windows Server 2000 オペレーティング システムを介したネットワーク クロックの同期の精度が向上しています。 さらに、Windows Server 2003 では、W32Time.dll で、タイムプロバイダーを使用したさまざまなハードウェア デバイスとネットワーク タイム プロトコルがサポートされました。

当初は Kerberos 認証用にクロック同期を提供するように設計されていましたが、現在のアプリケーションの多くでは、タイムスタンプを使用してトランザクションの一貫性が確保され、重要なイベントの時間やその他のビジネスクリティカルな時間的制約のある情報が記録されます。  Windows タイム サービスによって提供されるコンピューター間の時刻の同期は、これらのアプリケーションにとってメリットです。

## <a name="importance-of-time-protocols"></a>タイム プロトコルの重要性
タイム プロトコルでは、2 つのコンピューター間で通信して時間情報をやり取りし、その情報を使ってクロックを同期します。 Windows タイム サービスのタイム プロトコルを利用すると、クライアントではサーバーからの時間情報が要求され、受信された情報に基づいてそのクロックが同期されます。
  
Windows タイム サービスでは NTP を使用して、ネットワーク経由で時間を同期できます。 NTP は、時計を同期させるために必要な作業分野のアルゴリズムを含むインターネット時刻プロトコルです。 NTP は、Windows の一部のバージョンで使用される簡易ネットワーク タイム プロトコル (SNTP) よりも正確なタイム プロトコルです。ただし、W32Time では引き続き SNTP をサポートして、Windows 2000 などの SNTP ベースのタイム サービスを実行しているコンピューターとの下位互換を可能にしています。
## <a name="where-to-find-windows-time-service-configuration-related-information"></a>Windows タイム サービスの構成関連情報を検索する場所  
このガイドでは、Windows タイム サービスの構成については**説明していません**。 Windows タイム サービスを構成する手順について説明している各種のトピックは、Microsoft TechNet 上や Microsoft サポート技術情報にあります。 構成情報が必要な場合は、次のトピックを参考にすると、適切な情報を見つけることができます。  
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


> [!IMPORTANT]  
> Windows Server 2016 より前では、W32Time サービスは、精密な時間管理を必要とするアプリケーションのニーズを満たすように設計されていませんでした。  しかし、Windows Server 2016 の更新プログラムにより、1 ミリ秒の精度を実現するソリューションをドメインに実装できるようになりました。  詳しくは、[Windows 2016 の正確な時刻](accurate-time.md)および[高精度の環境に向けた Windows タイム サービスの構成を目的とするサポート範囲](support-boundary.md)に関する記事を参照してください。

## <a name="related-topics"></a>関連トピック
- [Windows 2016 の正確な時刻](accurate-time.md)
- [Windows Server 2016 の時間精度の向上](windows-server-2016-improvements.md)  
- [Windows タイム サービスのしくみ](How-the-Windows-Time-Service-Works.md)  
- [Windows タイム サービスのツールと設定](Windows-Time-Service-Tools-and-Settings.md)  
- [高精度の環境に向けた Windows タイム サービスの構成を目的とするサポート範囲](support-boundary.md)
- [マイクロソフト サポート技術情報の記事 902229](https://go.microsoft.com/fwlink/?LinkId=186066)
