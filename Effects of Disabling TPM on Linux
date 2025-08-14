🔹 Effects of Disabling TPM on Linux

## Encryption and Disk Security

If you use TPM-based encryption (like LUKS with TPM or systemd-cryptsetup), those features will no longer work.

Most users rely only on password-based encryption, so there’s usually no issue.

## Secure Boot / Measured Boot

TPM can be used for boot verification in some distributions.

In your case, initramfs and bootloader are manually controlled, so Linux will boot fine.

## Attestation & Anti-Tampering

TPM is used by some services to verify system integrity.

Disabling it only removes these extra integrity checks; most users don’t actively rely on them.

## Windows Side

Windows can still use TPM because the changes affect only Linux.

TPM-based features in Windows 10 Micro (e.g., BitLocker) remain functional.

## Performance

The ~1.5-minute boot delay is gone, so the system starts much faster.
