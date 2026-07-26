# PROYECTO PISOS

De donde podemos sacar información es en en la columna details__col-right con los divs de clase details__block.
## ANÁLISIS DE PÁGINA
### Navegación por url
El enlace principal es https://www.pisos.com y por un lado tenemos
- alquiler
- venta
- promociones: Obra nueva (En esta opcion se debe poner directamente - y localidad sin      especificar el tipo de construccion)
Después de seleccionar una de las dos opciones en el enlace, podemos poner (seguido de - y localidad):
- pisos: Casas y pisos
- casas: Casas y chalets
- piso: Pisos y apartamentos
- aticos
- duplexs
- estudios
- fincas_rusticas
- lofts
- locales: Locales y oficinas
- local_comercial
- almacen
- oficinas
- edificios
- naves
- naves_industriales
- naves_comerciales
- terrenos
- garajes: Garajes y trasteros
- trastero
- garaje

Después de poner - y localidad (sin acentos y sin ñ) se puede poner en cualquier orden:
- desde-{numero}: Precio mínimo
- hasta-{numero}: Precio máximo
- con-{numero}-habitaciones (o habitacion): Nº mínimo de habitaciones
- con-{numero}-banos (o bano): Nº mínimo de baños
- desde-{numero}-m2: Superficie mínima
- terraza
- ascensor
- jardin
- piscina
- garaje
- trastero
- calefaccion
- aireacondicionado
- confoto: Anuncios con foto
- preciorebajado
- ultimasemana
- ultimomes
- puertasabiertas
- anunciosexclusivos: Anuncios Recomendados
- inmuebleson: A estrenar
- fecharecientedesde-desc: Ordenados desde el más reciente
- asc: Ordenados por precio de forma ascendente
- desc: Ordenados por precio de forma descendente
- hab-desc: Ordenados por nº de habitaciones de forma descendente
- hab-asc: Ordenados por nº de habitaciones de forma ascendente
- m2-desc: Ordenados por m2 de superficie de forma descendente
- m2-asc: Ordenados por m2 de superficie de forma ascendente

Y al final de todo:
- ?keywords={palabra}

Despues de introducir en la url las opciones especificadas anteriormente, el div de clase grid__wrapper tiene dentro divs de clase ad-preview, en los cuales al hacer click de redirige a https://www.pisos.com/{lo que aparece en data-lnk-href}

### CARACTERÍSTICAS DE PISOS
* Superficie construída
* Superficie útil (No siempre aparece)
* Habitaciones
* Baños
* Planta
* Interior o Exterior
* Antigüedad
* Conservación: [Reformado, En buen estado, A reformar] (No siempre aparece)
* Gastos de Comunidad (No siempre aparece)
* Referencia