# orthogonal-blueprint

Skill untuk **orthogonal thinking** pada blueprint produk: stress-test ide, arsitektur sistem, dan keluar dari tunnel vision lewat boring-first gate, enam sumbu perspektif, tes orthogonality modul, peta reversibilitas, pre-mortem, dan kriteria falsifikasi.

## Isi folder

```text
SKILL.md          # Instruksi utama untuk agen
reference.md      # Lens per domain & anti-patterns (referensi)
```

Tidak ada skrip wajib; agen membaca `SKILL.md` dan mengikut taut ke `reference.md` bila perlu konteks domain.

## Pasang skill

Lewat CLI `skills` dengan nama skill:

```bash
npx skills@latest add rickyraz/skills --skill orthogonal-blueprint
```

Atau salin folder ini ke direktori skill editor Anda, misalnya `~/.cursor/skills/orthogonal-blueprint/` atau `.cursor/skills/orthogonal-blueprint/` di repo proyek.

## Apa yang dicakup skill ini

- Phase 0: **boring solution gate** sebelum menggeser perspektif
- Phase 1: permasalahan permukaan vs kebutuhan mendasar
- Phase 2: **enam sumbu** (inversion, abstraksi, constraint, temporal, adversarial, cross-domain)
- Phase 3 & 3.5: orthogonality modul dan klasifikasi reversibilitas (Type 1 / Type 2)
- Phase 4 & 4.5: audit myopia, pre-mortem, dan **falsification gate**
- Template output blueprint terstruktur dan checklist sign-off

## Referensi tambahan

- Detail lens (fintech, infra, hardware, web/mobile) dan daftar frasa yang harus ditantang: [`reference.md`](reference.md)

## Titik masuk

Mulai dari [`SKILL.md`](SKILL.md) (frontmatter `name: orthogonal-blueprint` untuk discovery).
