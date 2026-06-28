# Riset Warna dan Bentuk untuk Redesign VibeLink

Konteks keputusan: VibeLink mengubah suara lingkungan dan emosi bicara menjadi umpan balik visual + haptik untuk pengguna Deaf/Hard of Hearing (Deaf/HoH) dan pengguna neurodivergent, khususnya Autism Spectrum Disorder (ASD). Karena informasi utama dipindahkan dari kanal audio ke visual/haptik, estetika pastel + cream + aksen hitam hanya layak jika tidak mengorbankan kontras, redundansi makna, ukuran sentuh, dan kontrol sensorik [NIDCD](https://www.nidcd.nih.gov/health/assistive-devices-people-hearing-voice-speech-or-language-disorders), [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html), [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html).

## 1. Warna untuk pengguna Deaf / Hard of Hearing

Assistive devices untuk orang dengan gangguan pendengaran memakai sinyal visual dan getaran, misalnya alerting devices dengan lampu berkedip atau vibrasi; ini mendukung arah VibeLink yang memakai visual + haptik sebagai pengganti/pendamping audio [NIDCD](https://www.nidcd.nih.gov/health/assistive-devices-people-hearing-voice-speech-or-language-disorders). Dalam desain untuk Deaf/HoH, informasi visual bukan dekorasi: ia menjadi kanal utama untuk awareness, orientasi, dan respons; DeafSpace juga menekankan sensory reach, visual access, light/color, dan vibration sebagai bagian dari akses [Gallaudet DeafSpace](https://gallaudet.edu/campus-design-and-planning/deafspace/), [NIDCD](https://www.nidcd.nih.gov/health/assistive-devices-people-hearing-voice-speech-or-language-disorders).

Implikasinya: kontras dan kejelasan visual harus diperlakukan lebih ketat daripada UI umum [reasoning]. WCAG melarang warna sebagai satu-satunya cara menyampaikan informasi, meminta rasio kontras teks normal minimal 4.5:1, dan meminta kontras minimal 3:1 untuk komponen UI/non-teks yang perlu terlihat [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html), [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html), [WCAG 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html).

Palet pastel berisiko bila seluruh makna dikodekan lewat warna, karena pastel cenderung dekat luminansinya dengan cream/putih dan karena pengguna tidak boleh dipaksa membedakan status hanya dari hue [reasoning], [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html). Solusi VibeLink: setiap status suara/emosi harus punya kombinasi warna + ikon + bentuk + label teks + pola haptik, sehingga warna hanya mempercepat scan, bukan satu-satunya sumber makna [reasoning], [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html).

## 2. Warna untuk pengguna ASD

Pengguna autistic dapat mengalami hyper- atau hypo-sensitivity terhadap stimulus sensorik, termasuk visual; National Autistic Society mencatat bahwa pengalaman sensorik dapat memengaruhi rasa aman, stres, dan kemampuan memproses lingkungan [National Autistic Society](https://www.autism.org.uk/advice-and-guidance/topics/sensory-differences/sensory-differences/all-audiences). ASPECTSS, indeks desain autism oleh Magda Mostafa, menekankan pengendalian stimulus sensorik, sensory zoning, escape spaces, dan transisi yang dapat diprediksi; ini mendukung UI yang low-arousal, tidak ramai, dan mudah dipindai [ASPECTSS](https://www.autism.archi/aspectss).

Tidak ada aturan universal bahwa semua pengguna ASD selalu lebih nyaman dengan pastel tertentu; preferensi sensorik bersifat individual dan perlu opsi personalisasi [reasoning], [National Autistic Society](https://www.autism.org.uk/advice-and-guidance/topics/sensory-differences/sensory-differences/all-audiences), [W3C COGA](https://www.w3.org/TR/coga-usable/). Namun, dibanding warna sangat jenuh dan kontras dekoratif yang agresif, muted/pastel sebagai fill non-teks adalah default yang lebih sesuai dengan prinsip low-stimulation [reasoning], [ASPECTSS](https://www.autism.archi/aspectss), [W3C COGA](https://www.w3.org/TR/coga-usable/).

Warna yang perlu dihindari sebagai dominan: merah jenuh untuk area besar, kuning neon/intens, dan kombinasi high-saturation yang berkedip atau bergerak, karena visual intensity dan motion dapat menambah beban sensorik [reasoning], [National Autistic Society](https://www.autism.org.uk/advice-and-guidance/topics/sensory-differences/sensory-differences/all-audiences), [WCAG 2.3.3](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions.html). Latar cream/warm neutral lebih masuk akal daripada putih murni sebagai default karena mengurangi kesan glare tanpa menurunkan kontras teks gelap; mode gelap sebaiknya opsional, bukan satu-satunya default, karena kebutuhan visual tiap orang berbeda [reasoning], [W3C COGA](https://www.w3.org/TR/coga-usable/).

## 3. Kontras & WCAG dengan palet pastel di atas cream

Aturan utama: teks normal harus mencapai minimal 4.5:1; teks besar boleh 3:1; komponen UI penting dan indikator visual non-teks perlu 3:1 terhadap warna bersebelahan [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html), [WCAG 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html). WCAG juga menyatakan informasi tidak boleh bergantung pada warna saja [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html).

Hasil hitung rasio kontras WCAG untuk draft palet VibeLink [reasoning]:

| Pasangan | Rasio | Keputusan |
|---|---:|---|
| `#161616` di `#FFF8EE` | 17.16:1 | Lulus teks normal |
| `#161616` di `#B8E6C4` | 13.06:1 | Lulus teks normal |
| `#161616` di `#F6E6A8` | 14.48:1 | Lulus teks normal |
| `#161616` di `#F7C59F` | 11.58:1 | Lulus teks normal |
| `#161616` di `#F3A6A6` | 9.32:1 | Lulus teks normal |
| `#E96B95` di `#FFF8EE` | 2.84:1 | Gagal sebagai teks normal |
| `#B7D8F2` di `#FFF8EE` | 1.41:1 | Gagal sebagai teks normal |
| `#F7B7CF` di `#FFF8EE` | 1.58:1 | Gagal sebagai teks normal |
| `#BDE8CA` di `#FFF8EE` | 1.28:1 | Gagal sebagai teks normal |
| `#F7E7A3` di `#FFF8EE` | 1.18:1 | Gagal sebagai teks normal |

Kesimpulan kontras: pastel tidak boleh dipakai sebagai warna teks di atas cream; pastel harus dipakai sebagai fill/category coding saja, sementara teks, angka besar, ikon kritis, outline fokus, dan tombol utama harus memakai near-black atau warna gelap yang lulus kontras [reasoning], [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html), [WCAG 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html).

Untuk color-vision deficiency, National Eye Institute menjelaskan bahwa red-green color blindness adalah bentuk yang umum, termasuk deuteranomaly/deuteranopia dan protanomaly/protanopia [NEI](https://www.nei.nih.gov/learn-about-eye-health/eye-conditions-and-diseases/color-blindness). Karena itu, kuning-vs-hijau pastel dan oranye-vs-merah pastel dapat kabur untuk sebagian pengguna; pink-vs-biru biasanya lebih aman, tetapi tetap tidak boleh menjadi satu-satunya kode [reasoning], [NEI](https://www.nei.nih.gov/learn-about-eye-health/eye-conditions-and-diseases/color-blindness), [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html). Rekomendasi: setiap warna dipasangkan dengan ikon, bentuk status, label, dan pola haptik berbeda [reasoning], [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html).

## 4. Pemetaan warna emosi dalam skema pastel

Riset lintas-budaya menunjukkan ada pola umum dalam asosiasi warna-emosi, tetapi asosiasi itu juga dipengaruhi bahasa, geografi, dan budaya; maka pemetaan warna emosi boleh digunakan sebagai default, tetapi tidak boleh dianggap universal [Psychological Science](https://journals.sagepub.com/doi/10.1177/0956797620948810). Studi komputasional tentang asosiasi warna-emosi juga mendukung bahwa relasi warna-emosi tidak satu dimensi dan perlu dibaca sebagai probabilistik, bukan hukum tetap [Royal Society Open Science](https://royalsocietypublishing.org/doi/10.1098/rsos.190741).

Default VibeLink `green=positive`, `yellow=neutral`, `orange=frustrated`, `red=anger` masuk akal sebagai konvensi awal karena hijau sering dibaca aman/positif, kuning sebagai perhatian/netral-transisi, oranye sebagai eskalasi, dan merah sebagai marah/bahaya [reasoning], [Psychological Science](https://journals.sagepub.com/doi/10.1177/0956797620948810). Caveat: asosiasi warna harus user-editable, label emosi harus eksplisit, dan mode color-blind-friendly harus tersedia karena makna warna berubah lintas budaya dan kondisi visual [reasoning], [Psychological Science](https://journals.sagepub.com/doi/10.1177/0956797620948810), [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html), [NEI](https://www.nei.nih.gov/learn-about-eye-health/eye-conditions-and-diseases/color-blindness).

Rekomendasi pastel emosi, semua memakai label/ikon gelap `#161616` [reasoning]:

| Emosi | Fill | Label gelap di atas fill | Catatan |
|---|---|---:|---|
| Positive | `#B8E6C4` | 13.06:1 | Tenang, hijau tidak terlalu neon |
| Neutral | `#F6E6A8` | 14.48:1 | Kuning lembut, bukan kuning intens |
| Frustrated | `#F7C59F` | 11.58:1 | Oranye hangat, dibedakan dari anger dengan ikon/bentuk |
| Anger | `#F3A6A6` | 9.32:1 | Merah pastel, bukan merah alarm jenuh |

## 5. Bentuk / Shape yang cocok

Bentuk rounded/pill cocok untuk arah VibeLink karena riset psikologi visual menemukan preferensi terhadap objek melengkung dibanding objek bersudut tajam, dan sudut tajam sering dikaitkan dengan threat/aversive response [Bar & Neta, Psychological Science](https://doi.org/10.1111/j.1467-9280.2006.01759.x). Efek bouba-kiki juga menunjukkan asosiasi lintas-modal antara bentuk bulat dengan suara/label yang lebih lembut dan bentuk tajam dengan kesan lebih keras; ini mendukung penggunaan rounded forms untuk UI yang ingin terasa calm dan non-threatening [Ramachandran & Hubbard](https://doi.org/10.1037/0096-3445.130.3.526).

Untuk ASD, rounded shape bukan “terapi”, tetapi konsisten dengan prinsip low-arousal, predictable, dan non-threatening; hindari shape tajam sebagai dekorasi status emosional kecuali untuk sinyal bahaya yang benar-benar kritis [reasoning], [ASPECTSS](https://www.autism.archi/aspectss), [Bar & Neta, Psychological Science](https://doi.org/10.1111/j.1467-9280.2006.01759.x).

Ukuran target sentuh: Apple menyarankan area target sekitar 44x44 pt untuk kontrol yang mudah disentuh [Apple HIG Accessibility](https://developer.apple.com/design/human-interface-guidelines/accessibility). Android merekomendasikan touch target minimal 48x48 dp untuk elemen interaktif [Android Accessibility](https://developer.android.com/guide/topics/ui/accessibility/apps), [Material Accessibility](https://m3.material.io/foundations/accessible-design/accessibility-basics). WCAG 2.5.8 menetapkan minimum 24x24 CSS px untuk target size pada level AA, sedangkan WCAG 2.5.5 Enhanced memakai 44x44 CSS px pada level AAA [WCAG 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html), [WCAG 2.5.5](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html).

Big-number UI cocok untuk VibeLink bila angka digunakan sebagai status ringkas, misalnya intensitas suara, confidence, atau level emosi; tetapi teks harus tetap bisa diperbesar sampai 200% tanpa kehilangan konten/fungsi [reasoning], [WCAG 1.4.4](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html). Material 3 menyediakan type scale untuk display/headline/title/body/label sehingga angka besar sebaiknya memakai role display/headline, sementara label pendamping tetap memakai ukuran body/label yang terbaca [Material Type Scale](https://m3.material.io/styles/typography/type-scale-tokens).

## 6. Verdict + rekomendasi konkret untuk VibeLink

Verdict: estetika pastel + cream + aksen hitam layak untuk Deaf/HoH + ASD hanya jika pastel diperlakukan sebagai fill pendukung, bukan teks atau satu-satunya kode makna [reasoning], [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html), [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html). Untuk Deaf/HoH, UI harus visual-clear, redundant, dan cepat dipindai karena sinyal visual/haptik menjadi kanal utama [reasoning], [NIDCD](https://www.nidcd.nih.gov/health/assistive-devices-people-hearing-voice-speech-or-language-disorders). Untuk ASD, UI harus low-stimulation, predictable, adjustable, dan tidak mengandalkan warna jenuh/motion agresif [reasoning], [National Autistic Society](https://www.autism.org.uk/advice-and-guidance/topics/sensory-differences/sensory-differences/all-audiences), [ASPECTSS](https://www.autism.archi/aspectss), [WCAG 2.3.3](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions.html).

### Set warna rekomendasi

| Token | Hex | Pemakaian |
|---|---|---|
| Background cream | `#FFF8EE` | Latar utama |
| Ink / text utama | `#161616` | Semua teks, ikon kritis, angka besar |
| Border/focus dark | `#222222` | Outline fokus, separator penting |
| Primary accent pink | `#E96B95` | CTA fill/indikator primer; teks di atasnya harus `#161616`, bukan putih |
| Emotion positive | `#B8E6C4` | Fill + ikon + label “Positive” |
| Emotion neutral | `#F6E6A8` | Fill + ikon + label “Neutral” |
| Emotion frustrated | `#F7C59F` | Fill + ikon + label “Frustrated” |
| Emotion anger | `#F3A6A6` | Fill + ikon + label “Anger” |
| Category yellow | `#F7E7A3` | Kategori non-kritis + label gelap |
| Category pink | `#F7B7CF` | Kategori non-kritis + label gelap |
| Category blue | `#B7D8F2` | Kategori non-kritis + label gelap |
| Category green | `#BDE8CA` | Kategori non-kritis + label gelap |

Catatan implementasi: bila pastel fill berada di atas cream dan batas objek perlu dikenali sebagai kontrol, tambahkan border/focus/ikon `#161616` atau `#222222`, karena kontras pastel terhadap cream hanya sekitar 1.18-1.84:1 dan tidak cukup untuk indikator non-teks kritis [reasoning], [WCAG 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html).

### Must-do checklist

- Kontras: teks/angka/ikon kritis pakai `#161616` atau warna gelap lain yang lulus 4.5:1; jangan pakai pastel sebagai teks di atas cream [WCAG 1.4.3](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html).
- Redundant coding: setiap emosi/kategori punya warna + ikon + label + bentuk/pola; jangan mengandalkan warna saja [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html).
- Color-blind safety: sediakan mode alternatif untuk red-green CVD dan jangan menjadikan hijau/kuning/oranye/merah sebagai pembeda tunggal [NEI](https://www.nei.nih.gov/learn-about-eye-health/eye-conditions-and-diseases/color-blindness), [WCAG 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html).
- Reduced motion: animasi alert harus bisa dimatikan atau dibuat non-esensial; hindari flashing/gerak agresif pada status emosi [WCAG 2.3.3](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions.html).
- Adjustable text: dukung pembesaran teks sampai 200% tanpa kehilangan fungsi, terutama pada label emosi dan angka status [WCAG 1.4.4](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html).
- Adjustable haptics: intensitas, pola, dan frekuensi haptik harus bisa diatur karena kebutuhan sensorik Deaf/HoH dan ASD berbeda [reasoning], [NIDCD](https://www.nidcd.nih.gov/health/assistive-devices-people-hearing-voice-speech-or-language-disorders), [National Autistic Society](https://www.autism.org.uk/advice-and-guidance/topics/sensory-differences/sensory-differences/all-audiences).
- Touch targets: gunakan minimal 48x48 dp di Android, 44x44 pt di iOS, dan jangan turun di bawah minimum WCAG 24x24 CSS px untuk target interaktif [Android Accessibility](https://developer.android.com/guide/topics/ui/accessibility/apps), [Apple HIG Accessibility](https://developer.apple.com/design/human-interface-guidelines/accessibility), [WCAG 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html).
- Shape: gunakan rounded pill/card dengan radius konsisten; simpan bentuk tajam hanya untuk kondisi kritis yang benar-benar perlu salience tinggi [reasoning], [Bar & Neta, Psychological Science](https://doi.org/10.1111/j.1467-9280.2006.01759.x).

*Riset: Codex (web search) · supervised.*
