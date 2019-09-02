# Responsrevisjoner for NVDB API LES V3

### Responsrevisjon 1

* [Konsekvent bruk av veglenkesekvensid](https://github.com/nvdb-vegdata/nvdb-api-client/commit/3765e42a30728fb4efc023c2f72472a046ec20a2#diff-b5f334c16ceccbb3987030524a0e828cR95). Byttet alle tidligere "veglenkesekvens" med "veglenkesekvensid" der det gjelder id-en
* [Netelementid og netelementtype på lokasjonsegenskap er endret til veglenkesekvensid](https://github.com/nvdb-vegdata/nvdb-api-client/commit/3765e42a30728fb4efc023c2f72472a046ec20a2#diff-c8692b87f0a2cf670ba98f95c457a46aR135)
* [RelativPosisjon for punkt](https://github.com/nvdb-vegdata/nvdb-api-client/commit/bb4ecee0d488d8cc5f945521a7b1abc45c790709#diff-eab00036a45a9bd9e5ae0f6ef8892c77R22)
* Egenskaper har fått entydig egenskapstype for enum: Tekstenum, Heltallenum, Flyttallenum: [vegobjekter](https://github.com/nvdb-vegdata/nvdb-api-client/commit/60f0225bfd11c6e1887519f8b35d60b91e2f6e8d#diff-5411560551c353f26c91708d93e16413R19), [vegobjekttyper](https://github.com/nvdb-vegdata/nvdb-api-client/commit/df988953cf19d42ec69d45ff19c0f6f98340b6a8)
* [Samme feltnavn for egenskap.kvalitet og geometri.kvalitet](https://github.com/nvdb-vegdata/nvdb-api-client/commit/3765e42a30728fb4efc023c2f72472a046ec20a2#diff-c8692b87f0a2cf670ba98f95c457a46aR41)
* [Endret representasjon av Sving under stedfesting](https://github.com/nvdb-vegdata/nvdb-api-client/commit/2c125b926477dab9bbb4f4900b97c22ed44f7385)
