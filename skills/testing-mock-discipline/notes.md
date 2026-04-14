# Analisa Kritik Mocking (Dillon Mulroy) vs Best Practice Testing

## Ringkasan
Kritik Dillon Mulroy secara prinsip **valid**: module/file-system mocking yang berlebihan memang sering menurunkan kualitas test karena test menjadi dekat ke detail implementasi, bukan perilaku runtime.

## Bagian yang Kuat dari Kritiknya
- **Over-mocking menurunkan fidelity**: test bisa hijau walau wiring runtime rusak.
- **Smell desain**: kebutuhan mock kompleks sering menandakan dependency tersembunyi (global singleton, hard import) dan seam arsitektur lemah.
- **DI sebagai solusi struktural**: function/constructor injection membuat dependency eksplisit, lebih mudah diganti fake/real saat test.

## Nuansa Penting (Agar Tidak Menjadi Dogma)
- Mock **bukan selalu buruk**; mock tetap berguna untuk:
  - memicu edge/failure path sulit direproduksi,
  - memutus ketergantungan eksternal yang lambat/tidak stabil,
  - menguji orchestration yang memang butuh verifikasi interaksi.
- Masalah utama adalah **default mindset** (selalu module mock), bukan tool mocking itu sendiri.

## Sintesis Best Practice (2026)
1. Uji pure logic dengan unit test minim mock.
2. Uji boundary penting (DB/fs/http) lewat integration test hermetic bila memungkinkan.
3. Uji critical path via e2e untuk validasi wiring end-to-end.
4. Gunakan mock secara sempit dan eksplisit; hindari mock berlapis.
5. Refactor ke DI bila test setup didominasi `jest.mock`/`vi.mock`.

## Kebijakan Praktis yang Bisa Diadopsi Tim
- Jika test butuh >2 module mocks, evaluasi ulang abstraksi + pertimbangkan integration test.
- Prioritaskan assertion outcome (state/output/event), bukan urutan call internal.
- Larang global singleton langsung di domain/service layer; akses via injected interface.
- Jadikan module mocking “last resort”, bukan baseline.

## Sumber Primer
- Google Testing Blog: Don’t Overuse Mocks  
  https://testing.googleblog.com/2013/05/testing-on-toilet-dont-overuse-mocks.html
- Vitest `vi.mock` API  
  https://vitest.dev/api/vi.html
- Jest Manual Mocks  
  https://jestjs.io/docs/manual-mocks
- Testing Library Guiding Principles  
  https://testing-library.com/docs/guiding-principles
- Martin Fowler: Practical Test Pyramid  
  https://martinfowler.com/articles/practical-test-pyramid.html
