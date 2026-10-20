# A3 · Ficha de especificaciones: pantalla Inicio

Valores sacados del frame `activity_inicio` de la copia de Figma. Con el plan gratuito Dev Mode pide pasar a un plan de pago, así que los he leído en el panel Diseño, que muestra los mismos datos (colores, fuentes, medidas y auto layout). El frame mide 360 × 800 y está a 1x, así que **1 px de Figma = 1 dp** (medidas) **= 1 sp** (textos). Las fotos se exportan a 3x, que es la densidad xxhdpi.

## Colores

Nombre funcional (el del rol de Material 3) y valor en formato Android `#AARRGGBB`. La columna «Oscuro» sale de la pantalla `01-inicio-oscuro` del prototipo.

| Nombre (colors.xml) | Figma | Android | Oscuro | Dónde se usa |
|---|---|---|---|---|
| `surface` | #F4FBF8 | #FFF4FBF8 | #FF0E1513 | Fondo de la pantalla |
| `on_surface` | #161D1B | #FF161D1B | #FFDDE4E1 | Título, categorías, «Novedades», nombre y precio |
| `on_surface_variant` | #3F4947 | #FF3F4947 | #FFBEC9C6 | Iconos, texto del buscador, edades, etiquetas inactivas |
| `surface_container` | #E9EFED | #FFE9EFED | #FF1A211F | Tarjetas de producto y barra de navegación |
| `surface_container_high` | #E3EAE7 | #FFE3EAE7 | #FF252B2A | Fondo del buscador |
| `surface_container_highest` | #DDE4E1 | #FFDDE4E1 | #FF303635 | Tarjetas de categoría |
| `secondary_container` | #CCE8E2 | #FFCCE8E2 | #FF334B47 | Indicador de la pestaña activa |
| `secondary` | #4A635F | #FF4A635F | #FFB1CCC6 | Etiqueta activa «Inicio» |
| `primary` | #006A60 | #FF006A60 | #FF82D5C8 | Texto del botón «Ver todo» |
| `on_primary` | #FFFFFF | #FFFFFFFF | #FF003731 | Pareja de `primary` en el tema (no sale en Inicio) |
| `error` | #BA1A1A | #FFBA1A1A | #FFFFB4AB | Fondo del badge del carrito |
| `on_error` | #FFFFFF | #FFFFFFFF | #FF690005 | Número del badge |
| `surface_80` | #F4FBF8 al 80 % | #CCF4FBF8 | #CC0E1513 | Fondo del corazón encima de la foto |

### Transparencias

| Elemento | En Figma | Cálculo del canal alfa | En Android |
|---|---|---|---|
| Fondo del corazón | `surface`, opacidad 80 % | 0,80 × 255 = 204 → `CC` | `#CCF4FBF8` (`surface_80`) |
| Zonas del prototipo | #FFFFFF al 0 % | 0 × 255 = 0 → `00` | `#00FFFFFF`, no se programa |
| Iconos de estado del kit | capa con opacidad 0 | — | no se programa |

## Tipografías

Todas son Roboto (en `res/font`) y ninguna va en mayúsculas (`textAllCaps="false"`). El espaciado entre letras de Figma está en px y Android lo pide en em: **px ÷ tamaño de la letra**.

| Estilo (styles.xml) | Peso | Tamaño | Interlineado | Espaciado | Capas |
|---|---|---|---|---|---|
| `TitleLarge` | Regular 400 | 22 sp | 28 sp | 0 | `tv_titulo` |
| `BodyLarge` | Regular 400 | 16 sp | 24 sp | 0,5 px ÷ 16 = 0,03125 em | `et_buscar` |
| `TitleMedium` | Medium 500 | 16 sp | 24 sp | 0 | `tv_bebe`, `tv_nina`, `tv_nino`, `tv_novedades`, `tv_precio_producto` |
| `BodyMedium` | Regular 400 | 14 sp | 20 sp | 0 | `tv_*_edad`, `tv_nombre_producto` |
| `LabelLarge` | Medium 500 | 14 sp | 20 sp | 0,1 px ÷ 14 = 0,00714 em | `btn_ver_todo` |
| `LabelMedium` | Medium 500 | 12 sp | 16 sp | 0,5 px ÷ 12 = 0,04167 em | Etiquetas de `bnv_inicio` |
| `LabelSmall` | Medium 500 | 11 sp | 16 sp | 0,5 px ÷ 11 = 0,04545 em | `tv_badge_carrito` |

El interlineado se escribe con `android:lineHeight`, que existe desde la API 28; por eso el proyecto tiene esa API como mínima.

## Medidas (dp)

| Elemento | Tamaño | Posición y separaciones | Esquinas |
|---|---|---|---|
| `activity_inicio` | 360 × 800 | Márgenes laterales de 16 | — |
| `tb_inicio` | 360 × 64 | Arriba; el título empieza a 56 del borde (hueco del icono inicial oculto) | — |
| `ib_carrito` | 48 × 48 (icono 24) | A 4 del borde derecho, centrado en la barra | — |
| `tv_badge_carrito` | 16 × 16 | Encima del icono: 4 por debajo del borde del botón y a 10 de su lado derecho | 8 (círculo) |
| `ll_buscador` | 328 × 56 | 8 por debajo de la barra; iconos de 48 a 4 de cada lado; texto a 56 del inicio | 28 |
| `cv_bebe`, `cv_nina`, `cv_nino` | 104 × 120 | 16 por debajo del buscador; 8 entre tarjetas; título y edad centrados, con 2 entre ellos | 12 |
| `tv_novedades` | ancho libre × 24 | 24 por debajo de las categorías | — |
| `btn_ver_todo` | 86 × 48 (fondo de 40) | Pegado al margen derecho y centrado con «Novedades»; relleno de 16 a los lados | 20 |
| `cv_producto` | 156 × 284 (alto según el nombre) | 8 por debajo de «Novedades»; 16 entre tarjetas; relleno inferior de 12 | 12 |
| `iv_producto` | 156 × 196 | Arriba de la tarjeta; la foto se recorta con `centerCrop` | Las de la tarjeta |
| Textos del producto | ancho 132 | 8 por debajo de la foto; relleno de 12 a los lados; 4 entre nombre y precio | — |
| `ib_favorito` | 48 × 48 (icono 24, fondo 32) | Esquina superior derecha de la foto | 16 (círculo) |
| `bnv_inicio` | 360 × 64 | Abajo; indicador activo de 56 × 32; 4 entre icono y etiqueta | 16 (indicador) |
