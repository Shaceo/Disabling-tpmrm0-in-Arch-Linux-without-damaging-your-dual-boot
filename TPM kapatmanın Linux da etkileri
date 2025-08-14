🔹 TPM Devre Dışı Bırakmanın Linux Tarafındaki Etkileri

## Şifreleme ve Disk Güvenliği

LUKS veya systemd-cryptsetup gibi bazı şifreleme mekanizmalarında TPM kullanımı varsa, bu özellik artık çalışmaz.

Fakat çoğu kullanıcı şifrelemeyi sadece parola ile yapıyorsa herhangi bir sorun olmaz.

## Secure Boot / Measured Boot

TPM, bazı dağıtımlarda önyükleme doğrulaması için kullanılır.

Senin durumunda initramfs ve bootloader zaten manuel kontrol ediliyor, dolayısıyla Linux açılışında bir sorun olmayacak.

## Attestation & Anti-Tampering

TPM, sistem bütünlüğünü doğrulayan bazı servisler için kullanılır. Linux’ta çoğu kullanıcı bunu aktif kullanmaz.

Bu servisler devre dışı kaldığında sadece “ekstra güvenlik ölçümü” kaybolur.

## Windows Tarafı

Windows TPM’i hâlâ kullanabiliyor, çünkü değişiklik sadece Linux tarafında.

Windows 10 Micro sürümünde BitLocker veya diğer TPM tabanlı güvenlik özellikleri etkilenmez.

##Performans

Artık boot sırasında 1,5 dakika beklemeyecek ve sistem çok daha hızlı açılacak.
