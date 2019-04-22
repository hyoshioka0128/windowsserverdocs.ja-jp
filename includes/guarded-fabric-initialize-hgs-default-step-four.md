拇印を使用して HGS にすべての証明書を指定した場合は、これらの証明書の秘密キー HGS 読み取りアクセスを許可するように指示します。 インストールされているデスクトップ エクスペリエンス搭載サーバーで、次の手順を行います。

1.  ローカル コンピューターの証明書マネージャーを開きます (**certlm.msc**)
2.  証明書の検索 > を右クリックして > すべてのタスク > プライベート キーの管理
3.  **[追加]** をクリックします。
4.  オブジェクトの選択 ウィンドウで、次のようにクリックします**オブジェクトの種類**を有効にすると**サービス アカウント。**
5.  警告テキストに記載されているサービス アカウントの名前を入力します。 `Initialize-HgsServer`
6.  GMSA が秘密キーへの「読み取り」アクセスを確認します。

Server core では、秘密キーのアクセス許可の設定で支援するために PowerShell モジュールをダウンロードする必要があります。

1.  実行`Install-Module GuardedFabricTools`インターネット接続、または実行がある場合は、HGS サーバーで`Save-Module GuardedFabricTools`別のコンピューターと HGS サーバー経由で、モジュールのコピーで。
2.  `Import-Module GuardedFabricTools` を実行します。 これにより、PowerShell 内で見つかった証明書オブジェクトに追加のプロパティが追加されます。
3.  PowerShell での証明書の拇印を検索します。 `Get-ChildItem Cert:\LocalMachine\My`
4.  ACL を更新の警告テキストに示された独自の拇印とアカウントを使用して次のコードで、gMSA アカウントに置き換える`Initialize-HgsServer`します。

    ```powershell
    $certificate = Get-Item "Cert:\LocalMachine\1A2B3C..."
    $certificate.Acl = $certificate.Acl | Add-AccessRule "HgsSvc_1A2B3C" Read Allow
    ```

HSM を基盤の証明書を使用しているかに格納されている証明書、サード パーティのキー ストレージ プロバイダーにする手順は適用されません。 秘密キーの権限を管理する方法については、キー記憶域プロバイダーのドキュメントを参照してください。 場合によっては、承認がないか、証明書がインストールされている場合に、コンピューター全体に承認が提供されます。

<!-- Appears in guarded-fabric-initialize-hgs-ad-mode-default.md and guarded-fabric-initialize-hgs-tpm-mode-default.md
-->