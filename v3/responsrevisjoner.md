# Responsrevisjoner for NVDB API LES V3

### Responsrevisjon 0
Støtten for responsrevisjon 0 vil bli fjernet ca mars 2020.

### Responsrevisjon 1

* [Konsekvent bruk av veglenkesekvensid](https://github.com/nvdb-vegdata/nvdb-api-client/commit/3765e42a30728fb4efc023c2f72472a046ec20a2#diff-b5f334c16ceccbb3987030524a0e828cR95). Byttet alle tidligere "veglenkesekvens" med "veglenkesekvensid" der det gjelder id-en
* [Netelementid og netelementtype på lokasjonsegenskap er endret til veglenkesekvensid](https://github.com/nvdb-vegdata/nvdb-api-client/commit/3765e42a30728fb4efc023c2f72472a046ec20a2#diff-c8692b87f0a2cf670ba98f95c457a46aR123)
* Lokasjonsegenskap bruker [startposisjon og sluttposisjon](https://github.com/nvdb-vegdata/nvdb-api-client/commit/3765e42a30728fb4efc023c2f72472a046ec20a2#diff-b5f334c16ceccbb3987030524a0e828cR43) i stedet for fra_posisjon og til_posisjon
* [RelativPosisjon for punkt](https://github.com/nvdb-vegdata/nvdb-api-client/commit/bb4ecee0d488d8cc5f945521a7b1abc45c790709#diff-eab00036a45a9bd9e5ae0f6ef8892c77R22)
* Egenskaper har fått entydig egenskapstype for enum: Tekstenum, Heltallenum, Flyttallenum: [vegobjekter](https://github.com/nvdb-vegdata/nvdb-api-client/commit/60f0225bfd11c6e1887519f8b35d60b91e2f6e8d#diff-5411560551c353f26c91708d93e16413R19), [vegobjekttyper](https://github.com/nvdb-vegdata/nvdb-api-client/commit/df988953cf19d42ec69d45ff19c0f6f98340b6a8)
* [Feltnavn for geometri.kvalitet](https://github.com/nvdb-vegdata/nvdb-api-client/commit/6330a7f9a05864831d12619a96220187f850ee42#diff-6f9ed187bf7b5d1c57ca059ef52bc580R96) er endret slik at det blir likt som for kvalitet under egenskaper
* [Endret representasjon av Sving under stedfesting](https://github.com/nvdb-vegdata/nvdb-api-client/compare/d327b3617a5ed456cb0e26434fa4b67eb7fa22fb...e6efd1f4224b9847cb383dc440881921bdc0cfb0#diff-968a6ef945827879a8ff8aa78c06a7d9R1)
