# Bypass ILicenseV2ResultListener

```smali
    # ✅ BYPASS: Cek jika ini license verification (code = 1)
    const/4 v0, 0x1
    if-ne p1, v0, :cond_bypass

    # ⭐ Langsung return true untuk license check
    return v0

    :cond_bypass
    # ⭐ Lanjutkan ke kode original untuk transaction lainnya

```

[Example Implementation](https://github.com/QiubyZ/ApkModDocument/blob/fe2a99d7c6ba6526ea37e74dee6b02fe690a5337/PairiLicenseV2/ILicenseV2ResultListener%24Stub.smali#L113#L121)
