---
ms.assetid: 99a68050-8d19-4c58-ad86-e08a3dcdb4f7
title: 付録 L - 監視するイベント
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 07/30/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c245c5a6b2165385096f32713a92916236cdddfb
ms.sourcegitcommit: a3958dba4c2318eaf2e89c7532e36c78b1a76644
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719698"
---
# <a name="appendix-l-events-to-monitor"></a>付録 l:監視するイベント

>適用先:Windows Server

次の表に、イベントで提供される推奨事項に従って、環境内で監視する必要がありますを[侵害の兆候の監視の Active Directory](../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)します。 次の表では、"現在の Windows イベント ID"列は、メイン ストリーム サポートは、現在のバージョンの Windows および Windows Server で実装されているにイベント ID を一覧表示します。  
  
"従来の Windows イベント ID"列は、Windows XP を実行しているクライアント コンピューターなど、Windows の以前のバージョンに対応するイベント ID を一覧表示、またはそれ以前と Windows Server 2003 またはそれ以前を実行しているサーバー。 「潜在的な重要度」列の低いイベントを考慮するかどうかを識別する、中、高度攻撃、および「イベントの概要」列を検出するのには、イベントの簡単な説明を提供します。  
  
高の考えられる重要度は 1 つのイベントの発生を調べる必要があります。 中または低の考えられる重要度は、これらのイベントが予期せず、または測定期間で、想定される基準を大幅に超える番号で発生した場合のみ調査することを意味します。 すべての組織が、必須調査応答を要求する警告を作成する前に、環境内でこれらの推奨事項をテストする必要があります。 環境はそれぞれ異なり、およびその他の害のないイベントによる高の考えられる重要度で順位付けのイベントが発生します。  
  
|||||  
|-|-|-|-|  
|**現在の Windows イベント ID**|**従来の Windows イベント ID**|**考えられる重要度**|**イベントの概要**|  
|4618|なし|高|監視されるセキュリティ イベント パターンが発生しています。|  
|4649|なし|高|再生攻撃が検出されました。 構成が正しくないエラーのため無害な偽陽性があります。|  
|4719|612|高|システムの監査ポリシーが変更されました。|  
|4765|なし|高|SID の履歴がアカウントに追加されました。|  
|4766|なし|高|SID の履歴をアカウントに追加できませんでした。|  
|4794|なし|高|An attempt was made to set the Directory Services Restore Mode. (ディレクトリ サービス復元モードの設定が試行されました。)|  
|4897|801|高|役割の分離が有効化されました。|  
|4964|なし|高|特殊グループが新しいログオンに割り当てられました。|  
|5124|なし|高|OCSP レスポンダー サービスのセキュリティ設定が更新されました|  
|なし|550|中 ~ 高|考えられるのサービス拒否 (DoS) 攻撃|  
|1102|517|中 ~ 高|監査ログが消去されました|  
|4621|なし|中|管理者がシステムを CrashOnAuditFail から回復しました。 管理者以外のユーザーはログインできるようになりました。 一部の監査可能アクティビティが記録されていない可能性があります。|  
|4675|なし|中|SID がフィルター処理されました。|  
|4692|なし|中|データ保護マスター キーのバックアップが試みられました。|  
|4693|なし|中|データ保護マスター キーの回復が試みられました。|  
|4706|610|中|ドメインに新しい信頼が作成されました。|  
|4713|617|中|Kerberos ポリシーが変更されました。|  
|4714|618|中|暗号化データの回復ポリシーが変更されました。|  
|4715|なし|中|オブジェクトの監査ポリシー (SACL) が変更されました。|  
|4716|620|中|ドメインの信頼情報が変更されました。|  
|4724|628|中|An attempt was made to reset an account's password. (アカウントのパスワードをリセットしようとしました。)|  
|4727|631|中|セキュリティが有効なグローバル グループが作成されました。|  
|4735|639|中|セキュリティが有効なローカル グループが変更されました。|  
|4737|641|中|セキュリティが有効なグローバル グループが変更されました。|  
|4739|643|中|ドメイン ポリシーが変更されました。|  
|4754|658|中|セキュリティが有効なユニバーサル グループが作成されました。|  
|4755|659|中|セキュリティが有効なユニバーサル グループが変更されました。|  
|4764|667|中|セキュリティが無効なグループが削除されました|  
|4764|668|中|グループの種類が変更されました。|  
|4780|684|中|管理者グループのメンバのアカウントに ACL が設定されました。|  
|4816|なし|中|着信メッセージの解読の際に RPC が整合性違反を検出しました。|  
|4865|なし|中|信頼されたフォレスト情報のエントリが追加されました。|  
|4866|なし|中|信頼されたフォレスト情報のエントリが削除されました。|  
|4867|なし|中|信頼されたフォレスト情報のエントリが変更されました。|  
|4868|772|中|証明書マネージャーが保留中の証明書の要求を拒否しました。|  
|4870|774|中|証明書サービスが証明書を取り消しました。|  
|4882|786|中|証明書サービスのセキュリティ アクセス許可が変更されました。|  
|4885|789|中|証明書サービスの監査フィルターが変更されました。|  
|4890|794|中|証明書サービスの証明書マネージャーの設定が変更されました。|  
|4892|796|中|証明書サービスのプロパティが変更されました。|  
|4896|800|中|証明書データベースから 1 つ以上の行が削除されました。|  
|4906|なし|中|CrashOnAuditFail 値が変更されました。|  
|4907|なし|中|オブジェクトの監査設定が変更されました。|  
|4908|なし|中|特殊グループのログオン テーブルが変更されました。|  
|4912|807|中|ユーザー別の監査ポリシーが変更されました。|  
|4960|なし|中|IPsec は、整合性チェックに失敗した着信パケットを破棄しました。 この問題が解決しない場合は、ネットワークの問題や、このコンピューターへの転送中にそのパケットが変更されていることを示している可能性があります。 リモート コンピューターから送信されたパケットとこのコンピューターが受信するパケットが同じであることを確認してください。 このエラーも、他の IPsec 実装との相互運用性の問題を示している可能性があります。|  
|4961|なし|中|IPsec は、リプレイ チェックに失敗した着信パケットを破棄しました。 この問題が解決しない場合、このコンピューターに対するリプレイ攻撃を示している可能性があります。|  
|4962|なし|中|IPsec は、リプレイ チェックに失敗した着信パケットを破棄しました。 着信パケットのシーケンス番号が小さすぎたため、リプレイでないことを確認できませんでした。|  
|4963|なし|中|IPsec は、セキュリティで保護された着信クリア テキストを破棄しました。 これは通常、リモート コンピューターがこのコンピューターに通知せずに IPsec ポリシーを変更したためです。 スプーフィング攻撃の試みの可能性もあります。|  
|4965|なし|中|IPsec は、不適切なセキュリティ パラメーター インデックス (SPI) を持つパケットをリモート コンピューターから受信しました。 これは通常、正常に機能しないハードウェアによりパケットが破損しているために発生します。 これらのエラーが解決されない場合、リモート コンピューターから送信されたパケットとこのコンピューターが受信するパケットが同じであることを確認してください。 このエラーも、他の IPsec 実装との相互運用性の問題を示している可能性があります。 その場合、接続が妨害されているのでなければ、これらのイベントは無視できます。|  
|4976|なし|中|メイン モード ネゴシエーション中、IPsec が無効なネゴシエーション パケットを受信しました。 この問題が解決しない場合、ネットワークの問題や、このネゴシエーションの変更またはレプレイの試みを示している可能性があります。|  
|4977|なし|中|クイック モード ネゴシエーション中、IPsec が無効なネゴシエーション パケットを受信しました。 この問題が解決しない場合、ネットワークの問題や、このネゴシエーションの変更またはレプレイの試みを示している可能性があります。|  
|4978|なし|中|拡張モード ネゴシエーション中、IPsec が無効なネゴシエーション パケットを受信しました。 この問題が解決しない場合、ネットワークの問題や、このネゴシエーションの変更またはレプレイの試みを示している可能性があります。|  
|4983|なし|中|IPsec 拡張モード ネゴシエーションに失敗しました。 対応するメイン モード セキュリティ アソシエーションが削除されました。|  
|4984|なし|中|IPsec 拡張モード ネゴシエーションに失敗しました。 対応するメイン モード セキュリティ アソシエーションが削除されました。|  
|5027|なし|中|Windows ファイアウォール サービスで、ローカル記憶域からセキュリティ ポリシーを取得できませんでした。 このサービスでは、現在のポリシーが引き続き適用されます。|  
|5028|なし|中|Windows ファイアウォール サービスで、新しいセキュリティ ポリシーを解析できませんでした。 このサービスでは、現在適用されているポリシーが引き続き使用されます。|  
|5029|なし|中|Windows ファイアウォール サービスで、ドライバーの初期化に失敗しました。 このサービスでは、現在のポリシーが引き続き適用されます。|  
|5030|なし|中|Windows ファイアウォール サービスを開始できませんでした。|  
|5035|なし|中|Windows ファイアウォール ドライバーを開始できませんでした。|  
|5037|なし|中|Windows ファイアウォール ドライバで、重大なランタイム エラーが検出されました。 サービスを終了します。|  
|5038|なし|中|コードの整合性によって、ファイルのイメージ ハッシュが有効でないと判断されました。 このファイルは、無許可の変更によって破損しているか、無効なハッシュがディスク デバイス エラーの可能性を示している場合があります。|  
|5120|なし|中|OCSP レスポンダー サービスが開始されました|  
|5121|なし|中|OCSP レスポンダー サービスが停止しました|  
|5122|なし|中|OCSP レスポンダー サービスで変更された構成エントリ|  
|5123|なし|中|OCSP レスポンダー サービスで変更された構成エントリ|  
|5376|なし|中|資格情報マネージャーの資格情報がバックアップされました。|  
|5377|なし|中|資格情報マネージャーの資格情報がバックアップから復元されました。|  
|5453|なし|中|IKE and AuthIP IPsec Keying Modules (IKEEXT) サービスが開始されていないため、リモート コンピューターとの IPsec ネゴシエーションが失敗しました。|  
|5480|なし|中|IPsec サービスは、コンピューター上のネットワーク インターフェイスの完全なリストを取得できませんでした。 この結果、適用された IPsec フィルターによって提供される保護を一部のネットワーク インターフェイスが受けることができないため、潜在的なセキュリティ上のリスクが生じます。 IP セキュリティ モニター スナップインを使って問題を診断してください。|  
|5483|なし|中|IPsec サービスは、RPC サーバーを初期化できませんでした。 IPsec サービスを開始できませんでした。|  
|5484|なし|中|IPsec サービスで深刻な障害が発生したため、シャットダウンされました。 IPsec サービスがシャットダウンされると、コンピューターでのネットワーク攻撃のリスクが高まったり、コンピューターが潜在的なセキュリティ上のリスクにさらされる可能性があります。|  
|5485|なし|中|IPsec サービスは、ネットワーク インターフェイスのプラグ アンド プレイ イベントで一部の IPsec フィルターを処理できませんでした。 この結果、適用された IPsec フィルターによって提供される保護を一部のネットワーク インターフェイスが受けることができないため、潜在的なセキュリティ上のリスクが生じます。 IP セキュリティ モニター スナップインを使って問題を診断してください。|  
|6145|なし|中|グループ ポリシー オブジェクトのセキュリティ ポリシーの処理中に 1 つまたは複数のエラーが発生しました。|  
|6273|なし|中|ネットワーク ポリシー サーバーがユーザーのアクセスを拒否しました。|  
|6274|なし|中|ネットワーク ポリシー サーバーがユーザーの要求を破棄しました。|  
|6275|なし|中|ネットワーク ポリシー サーバーがユーザーのアカウント要求を破棄しました。|  
|6276|なし|中|ネットワーク ポリシー サーバーがユーザーを検疫しました。|  
|6277|なし|中|ネットワーク ポリシー サーバーがユーザーにアクセスを許可しましたが、ホストが定義済みの正常性ポリシーを満たしていなかったため、プロベーションしています。|  
|6278|なし|中|ホストが定義済みの正常性ポリシーを満たしていたため、ネットワーク ポリシー サーバーはユーザーにフル アクセスを許可しました。|  
|6279|なし|中|ネットワーク ポリシー サーバーは、認証の試行に繰り返し失敗したため、ユーザー アカウントをロックしました。|  
|6280|なし|中|ネットワーク ポリシー サーバーは、ユーザー アカウントのロックを解除しました。|  
|-|640|中|[全般] のアカウントのデータベースが変更されました|  
|-|619|中|サービス品質ポリシーの変更|  
|24586|なし|中|ボリュームへの変換エラーが発生しました|  
|24592|なし|中|%2 のボリュームに変換を自動的に再起動に失敗しました。|  
|24593|なし|中|メタデータの書き込み:%2 のボリュームのメタデータを変更するときにエラーが返されました。 エラーが引き続き発生する場合は、ボリュームを復号化します。|  
|24594|なし|中|メタデータの再構築します。%2 のボリュームのメタデータのコピーを書き込みの試みは失敗し、ディスクの破損が表示されます。 エラーが引き続き発生する場合は、ボリュームを復号化します。|  
|4608|512|低|Windows を起動しています。|  
|4609|513|低|Windows をシャットダウンしています。|  
|4610|514|低|ローカル セキュリティ機関によって、認証パッケージが読み込まれました。|  
|4611|515|低|信頼されたログオン プロセスがローカル セキュリティ機関に登録されています。|  
|4612|516|低|監査メッセージをキューに登録するために割り当てられた内部リソースをすべて使用したため、一部の監査が失われました。|  
|4614|518|低|通知パッケージがセキュリティ アカウント マネージャーにより読み込まれています。|  
|4615|519|低|LPC ポートの無効な使用。|  
|4616|520|低|システム時刻が変更されました。|  
|4622|なし|低|セキュリティ パッケージがローカル セキュリティ機関によって読み込まれました。|  
|4624|528,540|低|アカウントが正常にログオンしました。|  
|4625|529-537,539|低|アカウントがログオンに失敗しました。|  
|4634|538|低|アカウントがログオフされます。|  
|4646|なし|低|IKE の DoS 防止モードを開始します。|  
|4647|551|低|ユーザーがログオフを開始しました。|  
|4648|552|低|明示的な資格情報を使ったログオンが試行されました。|  
|4650|なし|低|IPsec メイン モード セキュリティ アソシエーションが確立されました。 拡張モードが確立されませんでした。 証明書認証が使われませんでした。|  
|4651|なし|低|IPsec メイン モード セキュリティ アソシエーションが確立されました。 拡張モードが確立されませんでした。 認証に証明書が使われませんでした。|  
|4652|なし|低|IPsec メイン モード ネゴシエーションに失敗しました。|  
|4653|なし|低|IPsec メイン モード ネゴシエーションに失敗しました。|  
|4654|なし|低|IPsec クイック モード ネゴシエーションが失敗しました。|  
|4655|なし|低|IPsec メイン モード セキュリティ アソシエーションが終了しました。|  
|4656|560|低|オブジェクトに対するハンドルが要求されました。|  
|4657|567|低|レジストリ値が変更されました。|  
|4658|562|低|オブジェクトに対するハンドルが閉じられました。|  
|4659|なし|低|オブジェクトに対するハンドルが削除を目的として要求されました。|  
|4660|564|低|オブジェクトが削除されました。|  
|4661|565|低|オブジェクトに対するハンドルが要求されました。|  
|4662|566|低|オブジェクトで操作は実行されませんでした。|  
|4663|567|低|オブジェクトへのアクセスが試行されました。|  
|4664|なし|低|ハード リンクの作成が試みられました。|  
|4665|なし|低|アプリケーションのクライアント コンテキストを作成しようとしました。|  
|4666|なし|低|アプリケーションが操作を試行しました。|  
|4667|なし|低|アプリケーションのクライアント コンテキストが削除されました。|  
|4668|なし|低|アプリケーションが初期化されました。|  
|4670|なし|低|オブジェクトのアクセス許可が変更されました。|  
|4671|なし|低|ブロックされた序数への TBS を介したアクセスがアプリケーションから試行されました。|  
|4672|576|低|新しいログオンに特権が割り当てられました。|  
|4673|577|低|特権のあるサービスが呼び出されました。|  
|4674|578|低|特権のあるオブジェクトで操作が試行されました。|  
|4688|592|低|新しいプロセスが作成されました。|  
|4689|593|低|プロセスが終了しました。|  
|4690|594|低|オブジェクトに対するハンドルの複製が試みられました。|  
|4691|595|低|オブジェクトへの間接アクセスが要求されました。|  
|4694|なし|低|監査可能な保護されたデータの保護が試みられました。|  
|4695|なし|低|監査可能な保護されたデータの保護解除が試みられました。|  
|4696|600|低|プライマリのトークンは、処理に割り当てられました。|  
|4697|601|低|サービスをインストールしようとしてください。|  
|4698|602|低|スケジュールされたタスクが作成されました。|  
|4699|602|低|スケジュールされたタスクが削除されました。|  
|4700|602|低|スケジュールされたタスクが有効になりました。|  
|4701|602|低|スケジュールされたタスクが無効になりました。|  
|4702|602|低|スケジュールされたタスクがアップデートされました。|  
|4704|608|低|ユーザー権限が割り当てられました。|  
|4705|609|低|ユーザー権限が削除されました。|  
|4707|611|低|ドメインの信頼が削除されました。|  
|4709|なし|低|IPsec サービスが開始されました。|  
|4710|なし|低|IPsec サービスが無効になりました。|  
|4711|なし|低|次のいずれかが含まれている可能性があります。PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーのローカルにキャッシュされたコピーをコンピューターで適用しました。 PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーをコンピューターで適用しました。 PAStore エンジンは、ローカル レジストリ記憶域の IPsec ポリシーをコンピューターで適用しました。 PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーのローカルにキャッシュされたコピーをコンピューターで適用できませんでした。 PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーをコンピューターで適用できませんでした。 PAStore エンジンは、ローカル レジストリ記憶域の IPsec ポリシーをコンピューターで適用できませんでした。 PAStore エンジンは、アクティブな IPsec ポリシーの一部のルールをコンピューターで適用できませんでした。 PAStore エンジンは、ディレクトリ記憶域の IPsec ポリシーをコンピューターで読み込むことができませんでした。 PAStore エンジンは、ディレクトリ記憶域の IPsec ポリシーをコンピューターで読み込みました。 PAStore エンジンは、ローカル記憶域の IPsec ポリシーをコンピューターで読み込むことができませんでした。 PAStore エンジンには、記憶域がローカル コンピューターの IPsec ポリシーが読み込まれます。PAStore エンジンは、アクティブな IPsec ポリシーへの変更をポーリングし、変更は検出されません。 |  
|4712|なし|低|IPsec サービスは、重大なエラーの可能性を検出しました。|  
|4717|621|低|アカウントに、システムのセキュリティ アクセスが許可されました。|  
|4718|622|低|アカウントから、システムのセキュリティ アクセスが削除されました。|  
|4720|624|低|ユーザー アカウントが作成されました。|  
|4722|626|低|ユーザー アカウントが有効化されました。|  
|4723|627|低|An attempt was made to change an account's password. (アカウントのパスワードを変更しようとしました。)|  
|4725|629|低|ユーザー アカウントが無効化されました。|  
|4726|630|低|ユーザー アカウントが削除されました。|  
|4728|632|低|セキュリティが有効なグローバル グループにメンバーが追加されました。|  
|4729|633|低|セキュリティが有効なグローバル グループのメンバーが削除されました。|  
|4730|634|低|セキュリティが有効なグローバル グループが削除されました。|  
|4731|635|低|セキュリティが有効なローカル グループが作成されました。|  
|4732|636|低|セキュリティが有効なローカル グループにメンバーが追加されました。|  
|4733|637|低|セキュリティが有効なローカル グループのメンバーが削除されました。|  
|4734|638|低|セキュリティが有効なローカル グループが削除されました。|  
|4738|642|低|ユーザー アカウントが変更されました。|  
|4740|644|低|ユーザー アカウントがロックアウトされました。|  
|4741|645|低|コンピューター アカウントが変更されました。|  
|4742|646|低|コンピューター アカウントが変更されました。|  
|4743|647|低|コンピューター アカウントが削除されました。|  
|4744|648|低|セキュリティが無効なローカル グループが作成されました。|  
|4745|649|低|セキュリティが無効なローカル グループが変更されました。|  
|4746|650|低|セキュリティが無効なローカル グループにメンバーが追加されました。|  
|4747|651|低|セキュリティが無効なローカル グループのメンバーが削除されました。|  
|4748|652|低|セキュリティが無効なローカル グループが削除されました。|  
|4749|653|低|セキュリティが無効なグローバル グループが作成されました。|  
|4750|654|低|セキュリティが無効なグローバル グループが変更されました。|  
|4751|655|低|セキュリティが無効なグローバル グループにメンバーが追加されました。|  
|4752|656|低|セキュリティが無効なグローバル グループのメンバーが削除されました。|  
|4753|657|低|セキュリティが無効なグローバル グループが削除されました。|  
|4756|660|低|セキュリティが有効なユニバーサル グループにメンバーが追加されました。|  
|4757|661|低|セキュリティが有効なユニバーサル グループのメンバーが削除されました。|  
|4758|662|低|セキュリティが有効なユニバーサル グループが削除されました。|  
|4759|663|低|セキュリティが無効なユニバーサル グループが作成されました。|  
|4760|664|低|セキュリティが無効なユニバーサル グループが変更されました。|  
|4761|665|低|セキュリティが無効なユニバーサル グループにメンバーが追加されました。|  
|4762|666|低|セキュリティが無効なユニバーサル グループのメンバーが削除されました。|  
|4767|671|低|ユーザー アカウントのロックが解除されました。|  
|4768|672,676|低|Kerberos 認証チケット (TGT) が要求されました。|  
|4769|673|低|Kerberos サービス チケットが要求されました。|  
|4770|674|低|Kerberos サービス チケットが更新されました。|  
|4771|675|低|Kerberos 事前認証が失敗しました。|  
|4772|672|低|Kerberos 認証チケット要求が失敗しました。|  
|4774|678|低|アカウントがログオンにマップされました。|  
|4775|679|低|アカウントをログオンにマップできませんでした。|  
|4776|680,681|低|ドメイン コントローラーがアカウントの資格情報の検証を試みました。|  
|4777|なし|低|ドメイン コントローラーがアカウントの資格情報の検証に失敗しました。|  
|4778|682|低|セッションは Window Station に再接続しました。|  
|4779|683|低|セッションは Window Station から切断されました。|  
|4781|685|低|アカウント名が変更されました。|  
|4782|なし|低|パスワード ハッシュをアカウントにアクセスされました。|  
|4783|667|低|基本アプリケーション グループが作成されました。|  
|4784|なし|低|基本アプリケーション グループが変更されました。|  
|4785|689|低|基本アプリケーション グループにメンバーが追加されました。|  
|4786|690|低|基本アプリケーション グループからメンバーが削除されました。|  
|4787|691|低|非メンバーは、基本アプリケーション グループに追加されました。|  
|4788|692|低|非メンバーは、基本アプリケーション グループから削除されました。|  
|4789|693|低|基本アプリケーション グループが削除されました。|  
|4790|694|低|LDAP クエリ グループが作成されました。|  
|4793|なし|低|パスワード ポリシー確認 API が呼び出されました。|  
|4800|なし|低|ワークステーションがロックされました。|  
|4801|なし|低|ワークステーションのロックが解除されました。|  
|4802|なし|低|スクリーン セーバーが起動しました。|  
|4803|なし|低|スクリーン セーバーが解除されました。|  
|4864|なし|低|名前空間の競合が検出されました。|  
|4869|773|低|証明書サービスが再送信された証明書の要求を受信しました。|  
|4871|775|低|証明書サービスが証明書失効リスト (CRL) を公開する要求を受信しました。|  
|4872|776|低|証明書サービスが証明書失効リスト (CRL) を公開しました。|  
|4873|777|低|証明書要求の拡張が変更されました。|  
|4874|778|低|証明書の要求の属性が変更されました。|  
|4875|779|低|証明書サービスがシャットダウンの要求を受信しました。|  
|4876|780|低|証明書サービスがバックアップを開始しました。|  
|4877|781|低|証明書サービスのバックアップが完了しました。|  
|4878|782|低|証明書サービスが復元を開始しました。|  
|4879|783|低|証明書サービスが復元を完了しました。|  
|4880|784|低|証明書サービスが開始されました。|  
|4881|785|低|証明書サービスが停止しました。|  
|4883|787|低|証明書サービスはアーカイブされたキーを取得しました。|  
|4884|788|低|証明書サービスがデータベースに証明書をインポートしました。|  
|4886|790|低|証明書サービスが証明書の要求を受信しました。|  
|4887|791|低|証明書サービスは、証明書の要求を承認して、証明書を発行しました。|  
|4888|792|低|証明書サービスは証明書の要求を拒否しました。|  
|4889|793|低|証明書サービスが証明書の要求の状態を保留中に設定しました。|  
|4891|795|低|証明書サービスの構成エントリが変更されました。|  
|4893|797|低|証明書サービスがキーをアーカイブしました。|  
|4894|798|低|証明書サービスはキーをインポートしてアーカイブしました。|  
|4895|799|低|証明書サービスが Active Directory ドメイン サービスに CA 証明書を発行しました。|  
|4898|802|低|証明書サービスがテンプレートを読み込みました。|  
|4902|なし|低|ユーザー別の監査ポリシー表が作成されました。|  
|4904|なし|低|セキュリティ イベントのソースを登録しようとしました。|  
|4905|なし|低|セキュリティ イベントのソースを登録解除しようとしました。|  
|4909|なし|低|TBS のローカル ポリシー設定が変更されました。|  
|4910|なし|低|Tb、グループ ポリシー設定が変更されました。|  
|4928|なし|低|Active Directory レプリカ ソースの名前付けコンテキストが確立されました。|  
|4929|なし|低|Active Directory レプリカ ソースの名前付けコンテキストが削除されました。|  
|4930|なし|低|Active Directory レプリカ ソースの名前付けコンテキストが変更されました。|  
|4931|なし|低|Active Directory レプリカ ターゲットの名前付けコンテキストが変更されました。|  
|4932|なし|低|Active Directory の名前付けコンテキストのレプリカの同期が開始しました。|  
|4933|なし|低|Active Directory の名前付けコンテキストのレプリカの同期が終了しました。|  
|4934|なし|低|Active Directory オブジェクトの属性がレプリケートされました。|  
|4935|なし|低|レプリケーション エラーが開始します。|  
|4936|なし|低|レプリケーション エラーが終了します。|  
|4937|なし|低|レプリカから残留オブジェクトが削除されました。|  
|4944|なし|低|次のポリシーは、Windows ファイアウォールの起動時にアクティブでした。|  
|4945|なし|低|Windows ファイアウォールの起動時に規則が表示されました。|  
|4946|なし|低|Windows ファイアウォールの例外の一覧が変更されました。 規則が追加されました。|  
|4947|なし|低|Windows ファイアウォールの例外の一覧が変更されました。 規則が変更されました。|  
|4948|なし|低|Windows ファイアウォールの例外の一覧が変更されました。 規則が削除されました。|  
|4949|なし|低|Windows ファイアウォールの設定が既定値に戻されました。|  
|4950|なし|低|Windows ファイアウォールの設定が変更されました。|  
|4951|なし|低|メジャー バージョン番号が Windows ファイアウォールで認識されなかったため、規則が無視されました。|  
|4952|なし|低|規則のマイナ バージョン番号が Windows ファイアウォールで認識されなかったため、規則の一部が無視されました。 規則のその他の部分は適用されます。|  
|4953|なし|低|Windows ファイアウォールで、解析できなかった規則が無視されました。|  
|4954|なし|低|Windows ファイアウォールのグループ ポリシー設定が変更されました。 新しい設定が適用されています。|  
|4956|なし|低|Windows ファイアウォールでアクティブなプロファイルが変更されました。|  
|4957|なし|低|Windows ファイアウォールで次の規則が適用されませんでした。|  
|4958|なし|低|このコンピューターで構成されていないアイテムを次の規則が参照しているために、Windows ファイアウォールで規則が適用されませんでした。|  
|4979|なし|低|IPsec メイン モードおよび拡張モードのセキュリティ アソシエーションが確立されました。|  
|4980|なし|低|IPsec メイン モードおよび拡張モードのセキュリティ アソシエーションが確立されました。|  
|4981|なし|低|IPsec メイン モードおよび拡張モードのセキュリティ アソシエーションが確立されました。|  
|4982|なし|低|IPsec メイン モードおよび拡張モードのセキュリティ アソシエーションが確立されました。|  
|4985|なし|低|トランザクションの状態が変更されました。|  
|5024|なし|低|Windows ファイアウォール サービスが正常に開始されました。|  
|5025|なし|低|Windows ファイアウォール サービスが停止しました。|  
|5031|なし|低|Windows ファイアウォール サービスは、ネットワーク上の着信接続のアプリケーションによる受け入れをブロックしました。|  
|5032|なし|低|Windows ファイアウォールでは、ネットワーク上の着信接続のアプリケーションによる受け入れをブロックしたことをユーザーに通知できませんでした。|  
|5033|なし|低|Windows ファイアウォール ドライバが正常に開始しました。|  
|5034|なし|低|Windows ファイアウォール ドライバーが停止しました。|  
|5039|なし|低|レジストリ キーが仮想化されました。|  
|5040|なし|低|IPsec 設定に変更が加えられました。 認証セットが追加されました。|  
|5041|なし|低|IPsec 設定に変更が加えられました。 認証セットが変更されました。|  
|5042|なし|低|IPsec 設定に変更が加えられました。 認証セットが追加されました。|  
|5043|なし|低|IPsec 設定に変更が加えられました。 接続セキュリティのルールが追加されました。|  
|5044|なし|低|IPsec 設定に変更が加えられました。 接続セキュリティのルールが変更されました。|  
|5045|なし|低|IPsec 設定に変更が加えられました。 接続セキュリティのルールが削除されました。|  
|5046|なし|低|IPsec 設定に変更が加えられました。 暗号セットが追加されました。|  
|5047|なし|低|IPsec 設定に変更が加えられました。 暗号セットが変更されました。|  
|5048|なし|低|IPsec 設定に変更が加えられました。 暗号セットが削除されました。|  
|5050|なし|低|プログラムで InetFwProfile.FirewallEnabled(False) への呼び出しを使用して Windows ファイアウォールを無効にしよう|  
|5051|なし|低|ファイルが仮想化されました。|  
|5056|なし|低|暗号化の自己テストが実行されました。|  
|5057|なし|低|暗号化のプリミティブ操作に失敗しました。|  
|5058|なし|低|キー ファイルの操作。|  
|5059|なし|低|キーの移行操作。|  
|5060|なし|低|検証操作に失敗しました。|  
|5061|なし|低|暗号化操作。|  
|5062|なし|低|カーネル モード暗号化の自己テストが実行されました。|  
|5063|なし|低|暗号化プロバイダーの操作が試行されました。|  
|5064|なし|低|暗号化コンテキストの操作が試行されました。|  
|5065|なし|低|暗号化コンテキストの変更が試行されました。|  
|5066|なし|低|暗号化関数の操作が試行されました。|  
|5067|なし|低|暗号化関数の変更が試行されました。|  
|5068|なし|低|暗号化関数のプロバイダーの操作が試行されました。|  
|5069|なし|低|暗号化関数のプロパティの操作が試行されました。|  
|5070|なし|低|暗号化関数のプロパティの変更が試行されました。|  
|5125|なし|低|要求が、OCSP レスポンダー サービスに送信されました|  
|5126|なし|低|OCSP レスポンダー サービスは、によって自動的に更新された証明書の署名|  
|5127|なし|低|OCSP 失効プロバイダーは、失効情報を正常に更新されました|  
|5136|566|低|ディレクトリ サービス オブジェクトが変更されました。|  
|5137|566|低|ディレクトリ サービス オブジェクトが作成されました。|  
|5138|なし|低|ディレクトリ サービス オブジェクトの削除が取り消されました。|  
|5139|なし|低|ディレクトリ サービス オブジェクトが移動されました。|  
|5140|なし|低|ネットワーク共有オブジェクトにアクセスがありました。|  
|5141|なし|低|ディレクトリ サービス オブジェクトが削除されました。|  
|5152|なし|低|Windows フィルタリング プラットフォームにより、パケットがブロックされました。|  
|5153|なし|低|より制限の厳しい Windows フィルタリング プラットフォーム フィルターにより、パケットがブロックされました。|  
|5154|なし|低|Windows フィルタリング プラットフォームにより、アプリケーションまたはサービスによるポートでの着信接続のリッスンが許可されました。|  
|5155|なし|低|Windows フィルタリング プラットフォームにより、アプリケーションまたはサービスによるポートでの着信接続のリッスンがブロックされました。|  
|5156|なし|低|Windows フィルタリング プラットフォームにより、接続が許可されました。|  
|5157|なし|低|Windows フィルタリング プラットフォームにより、接続がブロックされました。|  
|5158|なし|低|Windows フィルタリング プラットフォームにより、ローカル ポートへのバインドが許可されました。|  
|5159|なし|低|Windows フィルタリング プラットフォームにより、ローカル ポートへのバインドがブロックされました。|  
|5378|なし|低|要求された資格情報の委任がポリシーによって許可されませんでした。|  
|5440|なし|低|Windows フィルタリング プラットフォームのベース フィルター エンジンが起動したときに、次のコールアウトが存在していました。|  
|5441|なし|低|Windows フィルタリング プラットフォームのベース フィルター エンジンが起動したときに、次のフィルターが存在していました。|  
|5442|なし|低|Windows フィルタリング プラットフォームのベース フィルター エンジンが起動したときに、次のプロバイダーが存在していました。|  
|5443|なし|低|Windows フィルタリング プラットフォームのベース フィルター エンジンが起動したときに、次のプロバイダー コンテキストが存在していました。|  
|5444|なし|低|次の副層が、Windows フィルタ リング プラットフォーム ベース フィルタ エンジンの開始時に存在します。|  
|5446|なし|低|Windows フィルタリング プラットフォーム コールアウトが変更されました。|  
|5447|なし|低|Windows Filtering Platform フィルターが変更されました。|  
|5448|なし|低|Windows フィルタリング プラットフォーム プロバイダーが変更されました。|  
|5449|なし|低|Windows フィルタリング プラットフォーム コンテキストが変更されました。|  
|5450|なし|低|Windows Filtering Platform 副層が変更されました。|  
|5451|なし|低|IPsec クイック モード セキュリティ アソシエーションが確立されました。|  
|5452|なし|低|IPsec クイック モード セキュリティ アソシエーションが終了しました。|  
|5456|なし|低|PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーをコンピューターで適用しました。|  
|5457|なし|低|PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーをコンピューターで適用できませんでした。|  
|5458|なし|低|PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーのローカルにキャッシュされたコピーをコンピューターで適用しました。|  
|5459|なし|低|PAStore エンジンは、Active Directory 記憶域の IPsec ポリシーのローカルにキャッシュされたコピーをコンピューターで適用できませんでした。|  
|5460|なし|低|PAStore エンジンは、ローカル レジストリ記憶域の IPsec ポリシーをコンピューターで適用しました。|  
|5461|なし|低|PAStore エンジンは、ローカル レジストリ記憶域の IPsec ポリシーをコンピューターで適用できませんでした。|  
|5462|なし|低|PAStore エンジンは、アクティブな IPsec ポリシーの一部のルールをコンピューターで適用できませんでした。 IP セキュリティ モニター スナップインを使って問題を診断してください。|  
|5463|なし|低|PAStore エンジンは、アクティブな IPsec ポリシーへの変更をポーリングし、変更がないことを検出しました。|  
|5464|なし|低|PAStore エンジンは、アクティブな IPsec ポリシーへの変更をポーリングして変更を検出し、それらの変更を IPsec サービスに適用しました。|  
|5465|なし|低|PAStore エンジンは、IPsec ポリシーの強制再読み込みのコントロールを受け取り、コントロールを正常に処理しました。|  
|5466|なし|低|PAStore エンジンは、Active Directory IPsec ポリシーの変更をポーリングし、Active Directory に到達できないと判断したため、Active Directory IPsec ポリシーのキャッシュされたポリシーを代わりに使用します。 前回のポーリング以降 Active Directory IPsec ポリシーに加えられた変更を適用できませんでした。|  
|5467|なし|低|PAStore エンジンは、Active Directory IPsec ポリシーの変更をポーリングし、Active Directory に到達できると判断しましたが、ポリシーに変更がないことを検出しました。 Active Directory IPsec ポリシーのキャッシュされたコピーは使用されなくなりました。|  
|5468|なし|低|PAStore エンジンは、Active Directory IPsec ポリシーの変更をポーリングして、Active Directory に到達できると判断し、ポリシーの変更を検出したため、それらの変更を適用しました。 Active Directory IPsec ポリシーのキャッシュされたコピーは使用されなくなりました。|  
|5471|なし|低|PAStore エンジンは、ローカル記憶域の IPsec ポリシーをコンピューターで読み込みました。|  
|5472|なし|低|PAStore エンジンは、ローカル記憶域の IPsec ポリシーをコンピューターで読み込むことができませんでした。|  
|5473|なし|低|PAStore エンジンは、ディレクトリ記憶域の IPsec ポリシーをコンピューターで読み込みました。|  
|5474|なし|低|PAStore エンジンは、ディレクトリ記憶域の IPsec ポリシーをコンピューターで読み込むことができませんでした。|  
|5477|なし|低|PAStore エンジンは、クイック モード フィルターを追加できませんでした。|  
|5479|なし|低|IPsec サービスが正常にシャットダウンされました。 IPsec サービスがシャットダウンされると、コンピューターでのネットワーク攻撃のリスクが高まったり、コンピューターが潜在的なセキュリティ上のリスクにさらされる可能性があります。|  
|5632|なし|低|ワイヤレス ネットワーク認証が要求されました。|  
|5633|なし|低|ワイヤード (有線) ネットワーク認証が要求されました。|  
|5712|なし|低|リモート プロシージャ コール (RPC) が試行されました。|  
|5888|なし|低|COM+ カタログのオブジェクトが変更されました。|  
|5889|なし|低|COM+ カタログからオブジェクトが削除されました。|  
|5890|なし|低|COM+ カタログにオブジェクトが追加されました。|  
|6008|なし|低|前のシステムのシャット ダウンが予期されていませんでした。|  
|6144|なし|低|グループ ポリシー オブジェクトのセキュリティ ポリシーが適用されました。|  
|6272|なし|低|ネットワーク ポリシー サーバーがユーザーのアクセスを許可しました。|  
|なし|561|低|オブジェクトに対するハンドルが要求されました。|  
|なし|563|低|オブジェクトの削除のオープン|  
|なし|625|低|ユーザー アカウントの種類が変更されました|  
|なし|613|低|IPsec ポリシー エージェントを開始しました|  
|なし|614|低|IPsec ポリシー エージェントが無効になっています|  
|なし|615|低|IPsec ポリシー エージェント|  
|なし|616|低|IPsec ポリシー エージェントには、潜在的な重大なエラーが発生しました。|  
|24577|なし|低|開始ボリュームの暗号化|  
|24578|なし|低|停止したボリュームの暗号化|  
|24579|なし|低|完了したボリュームの暗号化|  
|24580|なし|低|ボリュームは開始の復号化|  
|24581|なし|低|停止したボリュームの暗号化解除|  
|24582|なし|低|完了したボリュームの暗号化解除|  
|24583|なし|低|ボリュームは開始のワーカー スレッドの変換|  
|24584|なし|低|ボリュームの変換のワーカー スレッドが一時的に停止しました|  
|24588|なし|低|%2 のボリュームに変換操作には、不良セクターのエラーが発生しました。 このボリューム上のデータを検証してください。|  
|24595|なし|低|%2 のボリュームには、不良クラスターが含まれています。 これらのクラスターは、変換中にスキップされます。|  
|24621|なし|低|初期状態をチェックします。%2 のボリューム変換のトランザクションをロールバックします。|  
|5049|なし|低|IPsec セキュリティ アソシエーションが削除されました。|  
|5478|なし|低|IPsec サービスが正常に開始しました。|  
  
> [!NOTE]  
> 参照してください[Windows セキュリティ監査イベント](https://www.microsoft.com/download/details.aspx?id=50034)多くのセキュリティ イベント Id とその意味の一覧についてはします。  
>
> 実行**wevtutil Microsoft-Windows-セキュリティ-監査 gp/ge/gm:true**イベント Id のすべてのセキュリティの非常に詳細な一覧を取得するには  
  
Windows セキュリティ イベント Id とその意味の詳細については、Microsoft サポート記事を参照してください。 [Windows 7 および Windows Server 2008 R2 でのセキュリティ イベントの説明](https://support.microsoft.com/kb/977519)します。 ダウンロードすることもできます[Windows 7 のセキュリティ監査イベントと Windows Server 2008 R2](https://www.microsoft.com/download/details.aspx?id=21561)と[Windows 8 および Windows Server 2012 のセキュリティ イベントの詳細](https://www.microsoft.com/download/details.aspx?id=35753)、詳細なイベント情報を提供しますスプレッドシート形式で参照されているオペレーティング システムです。  
