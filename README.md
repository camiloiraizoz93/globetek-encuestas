# Encuestas CSAT / NPS — Globetek Customer Success

Dos páginas estáticas que reciben la calificación del cliente y la registran en HubSpot.

- `csat.html` — satisfacción con la atención recibida (1 a 5 estrellas)
- `nps.html` — probabilidad de recomendar Globetek (0 a 10)

## Cómo funcionan

El cliente recibe un correo al cerrarse su ticket, con las estrellas (o los números)
como links. Toca una, y cae en la página correspondiente con su puntaje ya en la URL:

```
csat.html?score=4&t=<ticket_id>&email=<email>&lang=es
nps.html?score=9&email=<email>&lang=en
```

La página registra la respuesta al cargar, vía la API pública de submissions de
HubSpot, y le agradece. Un solo click para el cliente.

Sin parámetros, la página muestra la escala interactiva (así también sirve para
probar o para quien llegue directo al link).

`lang` acepta `es` o `en` — el correo lo pasa según el idioma del contacto en HubSpot.

## Por qué no vive en HubSpot

El plan de HubSpot de este portal no incluye CMS Hub ni Landing Pages, así que no hay
forma de hostear una página propia ahí. Estas dos páginas son estáticas justamente para
poder vivir en cualquier lado, sin backend ni base de datos.

El destino final es el sitio oficial de Globetek (`globetek.com`, WordPress) — este
hosting es temporal, para tener la encuesta funcionando mientras se coordina eso.

## Configuración

Los IDs de HubSpot están al principio del `<script>` de cada página. El portalId y el
GUID del form son públicos por diseño: es lo mismo que queda expuesto en cualquier
formulario embebido de HubSpot en cualquier sitio web. No hay ningún token ni credencial
en este repo.

| | |
|---|---|
| Portal | `50430632` |
| Form CSAT | `83bbde50-b729-4712-bbfd-e6fd8ed4fd0c` → `email`, `ticket_id`, `csat_score_zappy` |
| Form NPS | `e1b1805d-d4cf-4ea0-956f-65f846bc2edd` → `email`, `nps_score_zappy` |

⚠️ **El dominio donde se publiquen estas páginas tiene que estar registrado en HubSpot**
(Settings → Reports & Analytics → Tracking → Domains). Si no, HubSpot recibe las
respuestas pero las marca como spam y se pierden sin aviso.
