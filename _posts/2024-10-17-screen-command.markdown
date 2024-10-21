---
layout: post
title:  "Screen Komutu"
date:   2024-10-17 15:07:16 +0300
categories: linux, command
---
`screen` komutu, Linux ve Unix tabanlı işletim sistemlerinde kullanılan bir terminal yöneticisidir. Uzak bir sunucuya (SSH gibi) bağlandığınızda, işlemleri arka planda sürdürebilir ve oturumunuzu kapatsanız bile komutların çalışmaya devam etmesini sağlar. Ayrıca, tek bir terminal oturumu içinde birden fazla terminal penceresi açmanıza ve bu oturumlar arasında geçiş yapmanıza imkan tanır. Bu sayede, özellikle uzun süreli işlemler ve uzak sunucu yönetimi gibi senaryolarda büyük kolaylık sağlar.

## Başlıca Kullanım Alanları

1. **Uzak Sunucu Yönetimi:** Uzak sunucularda işlemleri terminali kapatsanız bile arka planda çalıştırır, tekrar bağlanabilirsiniz.
2. **Uzun Süreli İşlemler:** Büyük dosya kopyalama veya veri işleme gibi uzun işlemleri başlatıp terminalden ayrılabilirsiniz.
3. **Çoklu Terminal Oturumu:** Tek bir oturumda birden fazla terminal penceresi açıp farklı işlemler yürütebilirsiniz.
4. **Bağlantı Koptuğunda Devam:** Bağlantı koptuğunda işlemler kesilmez, tekrar bağlanarak devam edebilirsiniz.
5. **Paylaşımlı Oturumlar:** Birden fazla kullanıcının aynı terminali paylaşarak çalışmasını sağlar.

## Kurulumu

`screen` komutu genellikle birçok dağıtımda varsayılan olarak yüklü gelir, yüklü değilse aşağıdaki komutları kullanarak kurulabilir.

- Debian/Ubuntu Tabanlı Dağıtımlar:
  
  ```
  sudo apt update
  sudo apt install screen
  ```
  
- Red Hat/CentOS/Fedora:

  - Red Hat ve CentOS için

  ```
  sudo yum install screen   
  ```

  - Fedora için

  ```
  sudo dnf install screen
  ```

- Arch Linux:

  ```
  sudo pacman -S screen
  ```

> Kurulumun başarılı olup olmadığını anlamak için terminalde `screen --version` komutunu çalıştırabilirsiniz.

## Temel Komutlar

* `screen` yeni bir oturum başlatır.
* `screen -ls` ya da `screen -list` açık olan ekranları listeler
* `ctrl + a + d` screen oturumundan çıkarken kullanılır, tamamen kapatmadan arka plana alır
* `screen -S session` session ismiyle yeni bir oturum başlatır.
* `screen -r session` session oturumuna yeniden bağlanır. 
* `screen -dr session` başka bir terminalde aktifse oturumu sonlandırır ve session oturumuna yeniden bağlanır. 
* `ctrl +d` ya da `exit` var olan screen oturumunu kapatır.


Daha ayrıntılı bilgi için [Screen User’s Manual](https://www.gnu.org/software/screen/manual/) sayfasını ziyaret edebilirsiniz.

