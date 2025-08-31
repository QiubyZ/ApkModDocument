# Bypass ILicenseV2ResultListener
![ss](https://github.com/QiubyZ/ApkModDocument/blob/main/PairiLicenseV2/Screenshot_20250831-221800.png)

## Hint
Search **onTransact** in file *com/pairip/licensecheck/ILicenseV2ResultListener$Stub.smali*, this is example for **ILicenseV2ResultListener$Stub.smali**

```smali
method public onTransact(ILandroid/os/Parcel;Landroid/os/Parcel;I)Z
    .registers 8
    .annotation system Ldalvik/annotation/MethodParameters;
        accessFlags = {
            0x0,
            0x0,
            0x0,
            0x0
        }
        names = {
            "code",
            "data",
            "reply",
            "flags"
        }
    .end annotation

    .annotation system Ldalvik/annotation/Throws;
        value = {
            Landroid/os/RemoteException;
        }
    .end annotation

    .line 59
    const-string v0, "com.android.vending.licensing.ILicenseV2ResultListener"

    const/4 v1, 0x1

    if-lt p1, v1, :cond_d

    const v2, 0xffffff

    if-gt p1, v2, :cond_d

    .line 60
    invoke-virtual {p2, v0}, Landroid/os/Parcel;->enforceInterface(Ljava/lang/String;)V

    :cond_d
    if-eq p1, v1, :cond_1d

    const v2, 0x5f4e5446

    if-eq p1, v2, :cond_19

    .line 77
    invoke-super {p0, p1, p2, p3, p4}, Landroid/os/Binder;->onTransact(ILandroid/os/Parcel;Landroid/os/Parcel;I)Z

    move-result p1

    return p1

    .line 65
    :cond_19
    invoke-virtual {p3, v0}, Landroid/os/Parcel;->writeString(Ljava/lang/String;)V

    goto :goto_2c

    .line 70
    :cond_1d
    invoke-virtual {p2}, Landroid/os/Parcel;->readInt()I

    move-result p1

    .line 71
    sget-object p3, Landroid/os/Bundle;->CREATOR:Landroid/os/Parcelable$Creator;

    invoke-static {p2, p3}, Lcom/pairip/licensecheck/ILicenseV2ResultListener$Stub;->readTypedObject(Landroid/os/Parcel;Landroid/os/Parcelable$Creator;)Ljava/lang/Object;

    move-result-object p2

    check-cast p2, Landroid/os/Bundle;

    .line 72
    invoke-virtual {p0, p1, p2}, Lcom/pairip/licensecheck/ILicenseV2ResultListener$Stub;->verifyLicense(ILandroid/os/Bundle;)V

    :goto_2c
    return v1
.end method

```

Insert the smali code below into **ILicenseV2ResultListener$Stub.smali**

```smali
    # ✅ BYPASS: Cek jika ini license verification (code = 1)
    const/4 v0, 0x1
    if-ne p1, v0, :cond_bypass

    # ⭐ Langsung return true untuk license check
    return v0

    :cond_bypass
    # ⭐ Lanjutkan ke kode original untuk transaction lainnya

```


this is a [Example Implementation](https://github.com/QiubyZ/ApkModDocument/blob/fe2a99d7c6ba6526ea37e74dee6b02fe690a5337/PairiLicenseV2/ILicenseV2ResultListener%24Stub.smali#L113#L121) result.
