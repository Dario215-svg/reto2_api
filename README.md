# Reto 2: Pruebas de API (Rick and Morty API)

**Candidato:** Carlos Dario Lara Garcia (`@Dario215-svg`)   
**Evaluación:** Challenge Técnico Covalto - Test API  
**Endpoint Bajo Prueba:** `https://rickandmortyapi.com/api/character?page={1..3}`  

---

## Descripción 

Este repositorio contiene el script automatizado en **Python** (`contar_personajes.py`) desarrollado con **Pytest** y **Requests** (sin clientes manuales como Postman o Insomnia) para consumir de forma paginada las primeras **3 páginas (60 personajes)** de *The Rick and Morty API*.

El script reutiliza la conexión mediante `requests.Session()` y valida de extremo a extremo los 4 resultados esperados del reto técnico:

---

## 1. Criterios Técnicos Validados

| Etapa en el Script | Requerimiento del Reto | Implementación en Python (`assert`) | Estado |
| :--- | :--- | :--- | :---: |
| **`[1]` Tiempo de Respuesta** | Indicar el tiempo de respuesta de la API. | Medición individual en milisegundos (`ms`) por cada una de las 3 páginas (`response.elapsed.total_seconds() * 1000`), además del cálculo de tiempo total y promedio por página. |  Passed |
| **`[2]` Status Code** | Validar código de respuesta HTTP exitoso. | Comprobación estricta `assert response.status_code == 200` en cada una de las 3 peticiones paginadas. | Passed |
| **`[3]` Vivos y Muertos** | Consumir personajes principales vivos y validar vivos y muertos. | Identificación de los **5 personajes principales vivos** (`IDs 1 al 5`) y clasificación de los **60 personajes** en listas `vivos` (`Alive`), `muertos` (`Dead`) y `desconocidos` (`unknown`). | Passed |
| **`[4]` Tipos de Datos** | Validación de tipos de datos en el response obtenido. | Verificación de estructura raíz (`dict`), llaves `info` y `results` (`list`), y validación con `isinstance()` de las **12 propiedades** en los 60 personajes evaluados (**720 validaciones de tipo**). | Passed |

---

## 2. Resumen Estadístico de las 3 Páginas Evaluadas (60 Personajes)

| Métrica / Categoría Evaluada | Conteo Real (`Páginas 1 a 3`) | Detalle / Observaciones |
| :--- | :---: | :--- |
| **Páginas Consultadas** | **3 páginas** | `?page=1`, `?page=2` y `?page=3` (20 personajes por página) |
|  **Total de Personajes Evaluados** | **60 personajes** | Del `ID: 1` (*Rick Sanchez*) al `ID: 60` (*Calypso*) |
|  **Personajes Principales y Vivos** | **5 personajes** | `Rick Sanchez`, `Morty Smith`, `Summer Smith`, `Beth Smith`, `Jerry Smith` |
|  **Total Vivos (`Alive`)** | **27 personajes** | Incluye a los 5 protagonistas y 22 personajes adicionales vivos |
|  **Total Muertos (`Dead`)** | **20 personajes** | Validados con estado `"Dead"` dentro de las 3 páginas |
|  **Total Desconocidos (`unknown`)** | **13 personajes** | Validados con estado `"unknown"` dentro de las 3 páginas |
|  **Suma de Comprobación** | **60 / 60** | `27 Alive + 20 Dead + 13 unknown = 60 personajes` |

---

## 3. Validación de Esquema y Tipos de Datos (Contrato JSON)

Para cada uno de los **60 personajes**, el script comprueba estrictamente las siguientes 12 propiedades:

| Propiedad del Objeto (`char`) | Tipo Esperado (`isinstance`) | Validaciones Ejecutadas (3 Páginas) | Estado |
| :--- | :---: | :---: | :---: |
| `char["id"]` | `int` | 60 / 60 verificados | OK |
| `char["name"]` | `str` | 60 / 60 verificados |  OK |
| `char["status"]` | `str` | 60 / 60 verificados |  OK |
| `char["species"]` | `str` | 60 / 60 verificados |  OK |
| `char["type"]` | `str` | 60 / 60 verificados |  OK |
| `char["gender"]` | `str` | 60 / 60 verificados |  OK |
| `char["origin"]` | `dict` | 60 / 60 verificados |  OK |
| `char["location"]` | `dict` | 60 / 60 verificados |  OK |
| `char["image"]` | `str` | 60 / 60 verificados |  OK |
| `char["episode"]` | `list` | 60 / 60 verificados |  OK |
| `char["url"]` | `str` | 60 / 60 verificados |  OK |
| `char["created"]` | `str` | 60 / 60 verificados |  OK |

---

## 4. Evidencia de Ejecución en Consola (Output Real)

Al ejecutar `python -m pytest test_rick_and_morty.py -v -s`, se obtiene la siguiente salida en consola:

```text
================================================================================
 EJECUTANDO PRUEBA DE API: RICK AND MORTY (CUBRIENDO 3 PÁGINAS)
================================================================================

[1 y 2] MÉTRICAS DE TIEMPO DE RESPUESTA Y STATUS CODE POR PÁGINA:
--------------------------------------------------------------------------------
 -> Página  1 | Status Code: 200 | Tiempo de respuesta:  241.30 ms
 -> Página  2 | Status Code: 200 | Tiempo de respuesta:  118.45 ms
 -> Página  3 | Status Code: 200 | Tiempo de respuesta:  115.12 ms
--------------------------------------------------------------------------------
 [MÉTRICA GLOBAL] Tiempo Total: 474.87 ms | Promedio por página: 158.29 ms
 [COBERTURA]      Se descargaron 60 personajes de 3 páginas.

[3 y 4] VALIDACIÓN DE PERSONAJES (VIVOS / MUERTOS) Y TIPOS DE DATOS:
--------------------------------------------------------------------------------
 ID:   1 | Rick Sanchez                 | Estado: Alive    | Especie: Human        | Tipos: OK
 ID:   2 | Morty Smith                  | Estado: Alive    | Especie: Human        | Tipos: OK
 ID:   3 | Summer Smith                 | Estado: Alive    | Especie: Human        | Tipos: OK
 ID:   4 | Beth Smith                   | Estado: Alive    | Especie: Human        | Tipos: OK
 ID:   5 | Jerry Smith                  | Estado: Alive    | Especie: Human        | Tipos: OK
 ...
 ID:  58 | Brad                         | Estado: Alive    | Especie: Human        | Tipos: OK
 ID:  59 | Brad Anderson                | Estado: Dead     | Especie: Human        | Tipos: OK
 ID:  60 | Calypso                      | Estado: Dead     | Especie: Human        | Tipos: OK
--------------------------------------------------------------------------------

[RESUMEN DE VALIDACIÓN EN LAS 3 PÁGINAS (60 PERSONAJES)]
 -> Personajes Principales y Vivos (5): Rick Sanchez, Morty Smith, Summer Smith, Beth Smith, Jerry Smith
 -> Total Vivos (Alive)            (27)
 -> Total Muertos (Dead)           (20)
 -> Total Desconocidos (unknown)   (13)

[ ÉXITO ] ¡Todas las páginas, estados y tipos de datos fueron validados!
================================================================================
PASSED
