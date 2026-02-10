## Super masala: Onlayn kino platformasi – obuna turlari

Siz onlayn kino tomosha qilish platformasi (Netflix'ga o'xshash) uchun obuna tizimini yozmoqdasiz. Foydalanuvchilar turli tariflarga obuna bo'lishi mumkin: oddiy, talabalar uchun va oilaviy.

---

### 1. Asosiy obuna klassi

`Obuna` nomli asosiy klass yarating:

- atributlar:
  - `foydalanuvchi` (string)
  - `asosiy_narx` (oylik narx, masalan 100_000)
- metodlar:
  - `oylik_tolov()` – default bo'lib `asosiy_narx`ni qaytarsin
  - `tavsif()` – `"Foydalanuvchi: {foydalanuvchi}, Tarif: Oddiy, Oylik to'lov: {oylik_tolov()}"` satrini qaytarsin

---

### 2. Talabalar va Oilaviy tariflar (merosxo'rlik)

Quyidagi merosxo'r klasslarni yozing:

- `TalabaObunasi(Obuna)`:
  - qo'shimcha atribut: `talaba_id` (string)
  - oylik to'lovga 30% chegirma qo'llang:
    - `oylik_tolov()` metodini qayta yozing
    - `super().oylik_tolov()` dan foydalanib, asosiy narxni olib, 30% chegirma bilan qaytaring
  - `tavsif()` metodini qayta yozing:
    - `"Tarif: Talaba, Talaba ID: {talaba_id}, Oylik to'lov: ..."` ko'rinishida bo'lsin

- `OilaviyObuna(Obuna)`:
  - qo'shimcha atribut: `ekranlar_soni` (butun son, bitta obuna nechta ekranda parallel ishlashi)
  - qoidalar:
    - 1 ta ekran – oddiy narx (`super().oylik_tolov()`)
    - har bir qo'shimcha ekran uchun +20% qo'shimcha to'lov
      - masalan, `ekranlar_soni = 3` bo'lsa: narx = `asosiy_narx * (1 + 0.2 * (3 - 1))`
  - `oylik_tolov()` metodini qayta yozing va hisoblashda `super()` dan foydalaning
  - `tavsif()` metodini qayta yozing:
    - `"Tarif: Oilaviy, Ekranlar: {ekranlar_soni}, Oylik to'lov: ..."` ko'rinishida bo'lsin

---

### 3. Polimorfizm: umumiy oylik to'lovni hisoblash

`umumiy_oylik(obunalar)` nomli funksiya yozing:

- argument: `Obuna` (yoki undan meros olgan) obyektlardan iborat ro'yxat
- har bir obuna uchun `oylik_tolov()` metodini chaqiring
- ularning yig'indisini qaytaring

---

### 4. Namuna (kutilyotgan natija)

Quyidagi kod ishlaganda mantiqan to'g'ri natija chiqishi kerak (aniq sonlar sizning hisoblash formulangizga qarab bo'ladi, lekin tartib va mantiq shunaqa bo'lsin):

```python
o1 = Obuna("Ali", 100_000)
o2 = TalabaObunasi("Olim", 100_000, "T-001")
o3 = OilaviyObuna("Ibrohim", 100_000, 3)

print(o1.tavsif())
print(o2.tavsif())
print(o3.tavsif())

obunalar = [o1, o2, o3]
print("Umumiy oylik to'lov:", umumiy_oylik(obunalar))
```

**Vazifa:** Klasslarni shunday yozingki, yuqoridagi chaqiruvlar merosxo'rlik, `super()` va polimorfizmni chiroyli namoyish etsin va hayotiy obuna tizimi mantiqiga mos bo'lsin.


