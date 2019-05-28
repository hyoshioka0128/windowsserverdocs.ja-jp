---
Title: SMB:ファイルとプリンターの共有ポートが開く必要があります。
TOCTitle: 'SMB: File and printer sharing ports should be open'
ms.date: 07/02/2012
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: d761e4532a5be92d43e09904e9df8f2aa61b6bb8
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63738463"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB:ファイルとプリンターの共有ポートが開く必要があります。


更新:2011 年 2 月 2 日

適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012、Windows Server 2008 R2

*このトピックではベスト プラクティス アナライザー スキャンで検知した特定の問題に対処するためのものです。このトピックの情報は、ファイル サービス ベスト プラクティス アナライザーを実行する必要がありましたし、このトピックで取り上げて問題が発生しているコンピューターのみに適用してください。ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](http://go.microsoft.com/fwlink/?linkid=122786%0d%0a)します。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>オペレーティング システム</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>製品/機能</strong></p></td>
<td><p>ファイル サービス</p></td>
</tr>
<tr class="odd">
<td><p><strong>重要度</strong></p></td>
<td><p>エラー</p></td>
</tr>
<tr class="even">
<td><p><strong>カテゴリ</strong></p></td>
<td><p>構成</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>問題

> *ファイルとプリンターの共有のために必要なは、ファイアウォールのポート (ポート 445 と 139) を開けません。*

## <a name="impact"></a>影響

> *コンピューターは共有フォルダーやこのサーバー上の他のサーバー メッセージ ブロック (SMB) ベースのネットワーク サービスにアクセスできません。*

## <a name="resolution"></a>解決方法

> *コンピューターのファイアウォールを介して通信するファイルとプリンターの共有を有効にします。*

この手順を実行するには、**Administrators** グループのメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>ファイルとプリンターの共有を有効にするファイアウォール ポートを開く

1.  コントロール パネルを開き、[**システムとセキュリティ**、] をクリックし、 **Windows ファイアウォール**します。

2.  左側のウィンドウで次のようにクリックします。**詳細設定**、コンソール ツリーで、クリックと**受信の規則**します。

3.  **受信の規則**、ルールを見つける**ファイルとプリンターの共有 (NB セッション-)** と**ファイルとプリンターの共有 (SMB)** します。

4.  ルールごとに、ルールを右クリックしをクリックして**規則の有効化**します。

## <a name="additional-references"></a>その他の参照情報

[共有フォルダーと Windows ファイアウォール](http://technet.microsoft.com/en-us/library/cc731402.aspx)(http://technet.microsoft.com/en-us/library/cc731402.aspx)

