---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: "トラブルシューティング用コンピューターの構成"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 915b8d1133b3bee050f5eedce9e7ac445f833048
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-a-computer-for-troubleshooting"></a>トラブルシューティング用コンピューターの構成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>を特定し、Active Directory の問題を修正する高度なトラブルシューティング方法を使用する前に、トラブルシューティング用にコンピューターを構成します。 基本的な知識がある必要がありますも<token>nextref_longhorincludes > 概念、手順、およびツールをトラブルシューティングします。 </para>
    <para>Windows Server 2008 監視ツールの詳細については、次を参照してください、Step-by-Step パフォーマンスと信頼性の監視では、Windows Server 2008 用のガイド (<linkText>https://go.microsoft.com/fwlink/?LinkId=123737</linkText>https://go.microsoft.com/fwlink/?LinkId=123737).</para>
  </introduction>
  <section>
    <title>トラブルシューティングのための構成タスク</title>
    <content>
      <para>Active Directoryドメイン サービス (AD DS) をトラブルシューティングするのには、コンピューターを構成するには、次のタスクを実行:</para>
      <para>
        <link xlink:href="#BKMK_2">AD DS用にリモート サーバー管理ツールをインストール</link>
      </para>
      <para>
        <link xlink:href="#BKMK_3">構成の信頼性とパフォーマンス モニター</link>
      </para>
      <para>
        <link xlink:href="#BKMK_4">ログ レベルを設定</link>
      </para>
    </content>
    <sections>
      <section address="BKMK_2">
        <title>AD DS のリモート サーバー管理ツールをインストール</title>
        <content>
          <para>AD DS を管理するために使用する管理ツールが自動的にインストールされているドメイン コント ローラーを作成する AD DS をインストールするときにします。 実行しているメンバー サーバーで、[管理ツールをインストールするにはドメイン コント ローラーをドメイン コント ローラーではないコンピューターからリモートで管理する場合は、 <token>nextref_longhorincludes > または Service Pack 1 (SP1)、Windows Vista を実行しているコンピューター。 実行しているメンバー サーバー上で<token>nextref_longhorincludes >、Active Directory ドメイン サービス ツールをインストールするサーバー マネージャーで、リモート サーバー管理ツール (RSAT) 機能を使用します。 RSAT には、Windows Server 2003 で Windows サポート ツールが置き換えられます。 そのコンピューターにツールをダウンロードして Windows Vista Service Pack 1 (SP1) を実行しているコンピューターで Active Directory ドメイン サービス ツールをインストールすることもできます。</para>
          <para>RSAT をインストールする方法については、次を参照してください。 <link xlink:href="610ba7d9-51b5-4e14-9232-0510a9091aba">AD DS のリモート サーバー管理のツールをインストールする</link>します。</para>
        </content>
      </section>
      <section address="BKMK_3">
        <title>信頼性とパフォーマンス モニターを構成する</title>
        <content>
          <para>Windows Server 2008 には、Windows の信頼性とパフォーマンス モニターは、パフォーマンス ログとアラート、Server Performance Advisor の場合、システム モニターなどの以前のスタンドアロン ツールの機能を組み合わせたもの Microsoft 管理コンソール (MMC) スナップインが含まれています。このスナップインでは、データ コレクター セットおよびイベント トレース セッションをカスタマイズするためのグラフィカル ユーザー インターフェイス (GUI) を提供します。</para>
          <para>信頼性とパフォーマンス モニターも含まれていますシステムに対する変更を追跡し、システムの安定性の変更を比較して MMC スナップインの信頼性モニターの関係をグラフィカルに表示を提供します。</para>
        </content>
      </section>
      <section address="BKMK_4">
        <title>ログ レベルを設定</title>
        <content>
          <para>イベント ビューアーのディレクトリ サービス ログで受信した情報がトラブルシューティングのために十分でない場合は、ログ出力レベルを上げるで適切なレジストリ エントリを使用して <embeddedLabel>HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics</embeddedLabel>します。</para>
          <para>既定では、すべてのエントリのログ レベルに設定 <embeddedLabel>0</embeddedLabel>、最小限の情報を提供します。最高のログ レベルは <embeddedLabel>5</embeddedLabel>します。エントリのレベルを上げることをディレクトリ サービス イベント ログに記録する追加のイベントが発生します。</para>
          <para>診断エントリのログ出力レベルを変更する、次の手順を使用することができます。</para>
          <alert class="caution">
            <para>を直接編集しないレジストリ他の手段がない限り、ことをお勧めします。レジストリに対する変更は検証されません、レジストリ エディターまたは Windows 前に、それらが適用され、その結果、正しくない値を格納できます。回復不可能なエラーは、システムで、これがあります。可能であれば、レジストリを直接編集するのではなく、タスクを実行するのにグループ ポリシーまたは MMC スナップインなどの他の Windows ツールを使用します。レジストリを編集する必要がある場合、は、細心の注意を使用します。</para>
          </alert>
          <para>
            <embeddedLabel>要件</embeddedLabel>
          </para>
          <list class="bullet">
            <listItem>
              <para>内のメンバーシップ <embeddedLabel>Domain Admins</embeddedLabel>、相当するものでは、この手順を完了するために必要な最低限またはします。 <token>review_detailincludes></para>
            </listItem>
            <listItem>
              <para>ツール: Regedit.exe</para>
            </listItem>
          </list>
          <procedure>
            <title>診断エントリのログ出力レベルを変更する</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>をクリックして <ui>開始</ui>、をクリックして <ui>実行</ui>、種類 <userInput>regedit</userInput>、をクリックし <ui>OK</ui>します。</para>
                </content>
              </step>
              <step>
                <content>
                  <para>ログ記録を設定するエントリに移動 <embeddedLabel>HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics</embeddedLabel> します。</para>
                </content>
              </step>
              <step>
                <content>
                  <para>エントリをダブルクリックし <embeddedLabel>Base</embeddedLabel>、をクリックして <embeddedLabel>10 進</embeddedLabel>します。</para>
                </content>
              </step>
              <step>
                <content>
                  <para>で<embeddedLabel>値</embeddedLabel>から整数を入力 <embeddedLabel>0</embeddedLabel> を通じて <embeddedLabel>5</embeddedLabel>、をクリックし <ui>OK</ui> します。</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>


