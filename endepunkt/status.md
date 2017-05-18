



# GET /status

Tjeneste for å hente ulike statusparametere om APIet.

## Hent status

```
GET https://www.vegvesen.no/nvdb/api/v2/status
```

```json
{
    "datagrunnlag": {
        "sist_oppdatert": "2015-01-14T12:52:18+01:00"
    },
    "datakatalog": {
        "id": 706,
        "dato": "2014-11-28",
        "versjon": "2.01"
    }
}
```

<table>
<thead>
<tr>
<th>Felt</th>
<th>Beskrivelse</th>
</tr>
</thead>
<tbody>
<tr>
<td>datagrunnlag.sist_oppdatert</td>
<td>Angir når datagrunnlaget sist ble hentet fra NVDB-databasen.</td>
</tr>
<tr>
<td>datakatalog.id</td>
<td>Angir id til aktiv datakatalog-versjon.</td>
</tr>
<tr>
<td>datakatalog.versjon</td>
<td>Angir versjonsnummer til aktiv datakatalog-versjon.</td>
</tr>
<tr>
<td>datakatalog.dato</td>
<td>Angir når den aktive versjonen av datakatalogen ble gyldig.</td>
</tr>
</tbody>
</table>

