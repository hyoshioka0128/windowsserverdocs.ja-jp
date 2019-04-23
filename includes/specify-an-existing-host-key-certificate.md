または、独自の証明書を使用する場合は、拇印を指定できます。 複数のコンピューター証明書を共有したり、TPM または HSM にバインドされている証明書を使用する場合に役立ちます。 ことができます。 次に、TPM バインド証明書 (秘密キーを盗まれ、別のコンピューターで使用できないし、TPM 1.2 のみが必要です) を作成する例を示します。

```powersehll
$tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
```


<!-- Appears in set-up-hgs-for-always-encrypted-in-sql-server.md and guarded-fabric-create-host-key.md
-->