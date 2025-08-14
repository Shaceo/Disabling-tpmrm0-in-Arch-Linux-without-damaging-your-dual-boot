# Disabling-tpmrm0-in-Arch-Linux-without-damaging-your-dual-boot
Disabling tpmrm0 in Arch Linux without damaging your dual boot ( step by step )    <h2>English Below !!</h2>


<h1>Türkçe</h1><br><br>
TPM Bekleme Sorunu Çözümü – Özet
<h3>1️⃣ Sorunu Tanımlama</h3><br><br>

Açılışta A start job is running for /dev/tpmrm0 (~1min 30s) beklemesi vardı.

TPM, Windows’ta kullanılacak şekilde açık kalmalıydı.

Arch Linux’ta sadece açılış hızını artırmak amaçlandı.

<h3>2️⃣ Kernel Modülünü Engelleme</h3>

<h5>/etc/modprobe.d/blacklist-tpm.conf dosyası oluşturuldu:</h5>

<code>sudo nano /etc/modprobe.d/blacklist-tpm.conf</code>

<h5>İçine yazıldı:</h5>

<code>blacklist tpm<br>
blacklist tpm_tis<br>
blacklist tpm_tis_core<br>
blacklist tpm_crb<br>
blacklist tpm_infineon</code>


<h5>Initramfs yeniden oluşturuldu:</h5>

<code>sudo mkinitcpio -P</code>


##Bu adım kernel’in artık TPM modüllerini yüklemeye çalışmamasını sağladı.

<h5>Modülün engellendiği kontrol edildi:</h5>

<code>modprobe -n -v tpm</code>

##Çıktı boş olmalı (modül yüklenecek değil, engellenmiş).

<h3>3️⃣ Systemd Device ve Servislerini Engelleme</h3>

<h5> TPM cihazını bekleten systemd unit mask’lendi ve TPM servisi (systemd-tpm2d) devre dışı bırakıldı:</h5>

<code>sudo systemctl mask dev-tpmrm0.device
sudo systemctl disable systemd-tpm2d.service
sudo systemctl mask systemd-tpm2d.service</code>

##Bu adımlar, systemd’nin açılışta TPM’i beklememesini sağladı.


<h5>İleride Ayarları Geri Açmak İstersek:</h5>

<code>sudo systemctl unmask dev-tpmrm0.device<br>
sudo systemctl enable systemd-tpm2d.service<br>
sudo systemctl unmask systemd-tpm2d.service<br>
sudo rm /etc/modprobe.d/blacklist-tpm.conf<br>
sudo mkinitcpio -P
</code>
<h1> English </h1><br><br></h1>
TPM Wait Issue Solution – Summary

<h3>1️⃣ Identifying the Issue</h3>

At boot: A start job is running for /dev/tpmrm0 (~1min 30s) appeared.

TPM should remain enabled for Windows usage.

In Arch Linux, only the boot speed improvement was desired.

<h3>2️⃣ Blocking the Kernel Module</h3>

<h5>Create /etc/modprobe.d/blacklist-tpm.conf file:</h5>

<code>sudo nano /etc/modprobe.d/blacklist-tpm.conf</code>

<h5>Write inside:</h5>

<code>blacklist tpm<br>
blacklist tpm_tis<br>
blacklist tpm_tis_core<br>
blacklist tpm_crb<br>
blacklist tpm_infineon</code>

<h5>Rebuilt initramfs:</h5>

<code>sudo mkinitcpio -P</code>

##This ensures the kernel no longer tries to load TPM modules.

<h5>Check if the module is blocked:</h5>

<code>modprobe -n -v tpm</code>

##The output should be empty (the module is not loaded, it is blocked).

<h3>3️⃣ Disabling Systemd Device and Services</h3>

<h5>Mask the TPM device and disable the TPM service:</h5>

<code>sudo systemctl mask dev-tpmrm0.device<br>
sudo systemctl disable systemd-tpm2d.service<br>
sudo systemctl mask systemd-tpm2d.service</code>

##These steps ensure systemd does not wait for TPM at boot.

<h5>Restoring Settings in the Future:</h5>

<code>sudo systemctl unmask dev-tpmrm0.device<br>
sudo systemctl enable systemd-tpm2d.service<br>
sudo systemctl unmask systemd-tpm2d.service<br>
sudo rm /etc/modprobe.d/blacklist-tpm.conf<br>
sudo mkinitcpio -P</code>
