---
title: クライアントが接続できず、使用可能なライセンスがないというエラーが表示される
description: リモート デスクトップ接続での使用可能なライセンスがないというエラーのトラブルシューティング
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: f163908277b2ab8cc0e3bfbcbc4ae5e8001a2b4a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857175"
---
# <a name="clients-cant-connect-and-see-no-licenses-available-error"></a>クライアントが接続できず、"使用可能なライセンスがありません" というエラーが表示される

この状況は、RDSH サーバーとリモート デスクトップ ライセンス サーバーを含む展開に当てはまります。

まず、ユーザーに発生している動作がどちらであるかを特定します。

- 使用可能なライセンスがないか、使用可能なライセンスサーバーがないため、セッションが切断された。
- セキュリティ エラーのため、アクセスが拒否された。

ドメイン管理者として RD セッション ホストにサインインし、RD ライセンス診断機能を開きます。 次のようなメッセージを探します。

  - リモート デスクトップ セッション ホスト サーバーの猶予期間が過ぎましたが、RD セッション ホスト サーバーでライセンス サーバーが 1 台も構成されていません。 RD セッション ホスト サーバーにライセンス サーバーが構成されていないと、RD セッション ホスト サーバーへの接続は拒否されます。
  - ライセンス サーバー \<コンピューター名\> は使用できません。 This could be caused by network connectivity problems, the Remote Desktop Licensing service is stopped on the license server, or RD Licensing isn't available. (原因としては、ネットワーク接続に問題がある、ライセンス サーバー上でリモート デスクトップ ライセンス サービスが停止している、または RD ライセンスが使用できない、の 3 つが考えられます。)

これらの問題は、次のユーザー メッセージと関連することがよくあります。

  - このコンピューターで利用できるリモート デスクトップ クライアント アクセス ライセンスがないため、リモート セッションは切断されました。
  - ライセンスを提供するためのリモート デスクトップ ライセンス サーバーがないため、リモート セッションは切断されました。

この場合は、[RD ライセンス サービスを構成](#configure-the-rd-licensing-service)します。

RD ライセンス診断機能ツールで、"RDP プロトコル コンポーネント X.224 により、プロトコル ストリームにエラーが検出され、クライアントが切断されました" のような他の問題が表示される場合は、ライセンスの証明書に影響を与える問題が存在する可能性があります。 そのような問題は、次のようなユーザー メッセージと関連することがよくあります。

Because of a security error, the client could not connect to the Terminal server. After making sure that you are signed in to the network, try connecting to the server again. (セキュリティのエラーのため、クライアントはターミナル サーバーに接続できません。ネットワークにサインインしていることを確認した後、もう一度サーバーに接続してみてください。)

この場合は、[X509 証明書のレジストリ キーを更新](#refresh-the-x509-certificate-registry-keys)します。

## <a name="configure-the-rd-licensing-service"></a>RD ライセンス サービスを構成する

次の手順では、サーバー マネージャーを使って、構成を変更します。 サーバー マネージャーを構成して使用する方法については、「[サーバー マネージャー](../../../administration/server-manager/server-manager.md)」をご覧ください

1. **[サーバー マネージャー]** を開き、 **[リモート デスクトップ サービス]** に移動します。
2. **[展開の概要]** で **[タスク]** を選択した後、 **[Edit Deployment Properties]\(展開のプロパティの編集\)** を選択します。
3. **[RD ライセンス]** を選択してから、展開に適したライセンス モードを選択します ( **[接続デバイス数]** または **[接続ユーザー数]** )。
4. RD ライセンス サーバーの完全修飾ドメイン名 (FQDN) を入力し、 **[追加]** を選択します。
5. 複数の RD ライセンス サーバーがある場合は、サーバーごとに手順 4 を繰り返します。 
    ![サーバー マネージャーでの RD ライセンス サーバーの構成オプション。](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

## <a name="refresh-the-x509-certificate-registry-keys"></a>X509 証明書のレジストリ キーを更新する

> [!IMPORTANT]  
> このセクションの手順には、慎重に従ってください。 レジストリに正しくない変更を加えると、重大な問題が発生する可能性があります。 レジストリの変更を開始する前に、[レジストリをバックアップ](https://support.microsoft.com/help/322756)して、何らかの問題が発生した場合に復元できるようにします。

この問題を解決するには、レジストリをバックアップした後、X509 証明書のレジストリ キーを削除し、コンピューターを再起動してから、RD ライセンス サーバーを再びアクティブ化します。 次の手順に従います。

> [!NOTE]
> RDSH サーバーごとに、次の手順を実行します。

RD ライセンス サーバーを再アクティブ化する方法は、次のとおりです。

1. レジストリ エディターを開き、**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM** に移動します。
2. [レジストリ] メニューで **[レジストリ ファイルのエクスポート]** を選択します。
3. **[ファイル名]** ボックスに「**exported- Certificate**」と入力し、 **[保存]** を選択します。
4. 次の各値を右クリックして **[削除]** を選択し、 **[はい]** を選択して削除を確認します。  
      - **証明書**
      - **X509 Certificate**
      - **X509 Certificate ID**
      - **X509 Certificate2**
5. レジストリ エディターを終了し、RDSH サーバーを再起動します。