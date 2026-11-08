# NekoUpdateChannel

NekoHub uygulamasının **güncelleme kanalı**. NekoHub açılışta bu repodaki `repos.json` dosyasını indirir ve hangi projelerin yönetileceğini buradan öğrenir.

- Ham dosya: `https://raw.githubusercontent.com/ekrem6161/NekoUpdateChannel/main/repos.json`
- Yeni proje eklemek için sadece `repos.json`'a bir kayıt ekleyip `main` dalına push et.

## repos.json şeması

| Alan | Zorunlu | Açıklama |
|---|---|---|
| `name` | ✅ | Proje adı (klasör adı olarak da kullanılır) |
| `url` | ✅ | GitHub repo adresi (ZIP ve `VERSION.TXT` buradan alınır) |
| `fqbn` | ❌ | Arduino kart tipi, örn. `arduino:avr:uno`. Boşsa firmware yönetilmez |
| `firmwarePath` | ❌ | Repo içindeki sketch klasörü, örn. `firmware/NekoM550D` |
| `pcApp` | ❌ | Repo içindeki PC uygulaması klasörü, örn. `pc/NekoM550D.Monitor`. Boşsa PC yazılımı yönetilmez |

### Örnek

```json
[
  {
    "name": "NekoM550D",
    "url": "https://github.com/ekrem6161/NekoM550D",
    "fqbn": "arduino:avr:uno",
    "firmwarePath": "firmware/NekoM550D",
    "pcApp": "pc/NekoM550D.Monitor"
  }
]
```

## Sürüm kuralı

Her proje reposunun **kökünde** `VERSION.TXT` bulunmalı ve içinde sadece sürüm numarası yazmalı:

```
1.2.8
```

NekoHub bu dosyayı kurulu sürümle karşılaştırır. Yeni sürüm yayınlamak = `VERSION.TXT` içeriğini artırıp push etmek.

## Proje türleri

- **Yalnız firmware:** `fqbn` + `firmwarePath` dolu, `pcApp` boş.
- **Yalnız PC yazılımı:** `pcApp` dolu, `fqbn` ve `firmwarePath` boş.
- **İkisi birlikte:** tüm alanlar dolu (ör. NekoM550D).
