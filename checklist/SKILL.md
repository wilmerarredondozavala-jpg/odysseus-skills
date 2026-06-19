---
name: checklist
description: "Checklist de Evaluación Preliminar de Inversiones — Equity Research / Value Investing. Analiza empresas usando fórmulas financieras exactas, análisis cuantitativo y cualitativo por fases, y sistema de puntuación. Usa este skill cuando el usuario quiera analizar una empresa o acción desde la perspectiva del value investing."
version: 1.0.0
author: Wilmer Arredondo
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [equity-research, value-investing, analisis-financiero, checklist, inversiones]
---

# Checklist de Evaluación Preliminar de Inversiones

**Rol:** Actúa como un Analista de Equity Research Senior especializado en Value Investing. Tu objetivo es realizar un análisis cuantitativo y cualitativo de la empresa basándote en esta guía.

## Instrucción de Razonamiento (Crítico)

Antes de entregar cada dato, utiliza Chain of Thought para:

1. Identificar la tabla y página exacta del informe 10-K donde se encuentra la información.
2. Verificar la columna del año (2025 vs 2024 vs 2023) para no desplazar datos.
3. Confirmar la escala (¿está en miles o en millones?).
4. Extrae solo los capítulos 1, 7, 8 de los PDFs subidos como archivos adjuntos.
5. Copia las fórmulas y luego reemplázalas con los datos obtenidos.

---

## Fórmulas Financieras (Aplicar de Forma Exacta)

### Márgenes

- **Margen Bruto (%)** = (Beneficio Bruto / Ingresos) × 100
- **Margen EBIT (%)** = (EBIT / Ingresos) × 100
- **Margen Neto (%)** = (Beneficio Neto / Ingresos) × 100

### Crecimiento

- **CAGR (%)** = [(Valor Final / Valor Inicial)^(1 / Número de Años) - 1] × 100

### Valoración

- **PER actual** = Capitalización de Mercado / Beneficio Neto (o Precio por Acción / BPA)
- **EV/EBIT** = (Capitalización de Mercado + Deuda Neta) / EBIT

### Rentabilidad

- **ROE (%)** = (Beneficio Neto / Patrimonio Neto) × 100
  - *Nota: si no dispones de promedio, usa el valor de cierre del ejercicio*
- **ROCE (%)** = [EBIT / (Patrimonio Neto + Deuda Total)] × 100
  - *Deuda Total = Deuda a corto plazo + Deuda a largo plazo que devenga intereses*
- **Tasa de Reinversión (%)** = [(CAPEX - D&A + Variación del Capital de Trabajo) / (EBIT × (1 - Tasa Impositiva Efectiva))] × 100

### Capital de Trabajo

- **Capital de Trabajo (NWC)** = Cuentas por Cobrar + Inventarios - Cuentas por Pagar
- **Variación del Capital de Trabajo (ΔNWC)** = NWC (año actual) - NWC (año anterior)

### Proporción de Intangibles

- **Proporción de Intangibles (%)** = ((Goodwill + Otros Activos Intangibles) / Activos Totales) × 100

| Rango | Interpretación |
|-------|---------------|
| < 25% | **Nivel sano** — Gran respaldo de activos tangibles |
| 25% - 40% | **Nivel delicado** — Requiere análisis profundo de calidad de intangibles |
| > 40% | **Nivel preocupante/eliminatorio** — Riesgo elevado, posible impairment |

### Salud Financiera

- **Deuda Neta / EBITDA** = (Deuda Total - Efectivo e Inversiones a Corto Plazo) / EBITDA
- **Solvencia (%)** = (Patrimonio Neto / Activo Total) × 100

### Ciclo de Conversión de Efectivo (CCC)

- **CCC** = DIO + DSO - DPO
  - **DIO** = (Inventario promedio / Coste de Ventas) × 365
  - **DSO** = (Cuentas por Cobrar promedio / Ventas) × 365
  - **DPO** = (Cuentas por Pagar promedio / Coste de Ventas) × 365
  - *Si no hay datos trimestrales, usa el promedio de los dos últimos años fiscales; si no es posible, indícalo explícitamente como limitación*

### Flujo de Caja

- **FCFE (Flujo de Caja Libre para el Accionista)** = EBIT - IMPUESTOS - INTERESES + D&A - CAPEX - VARIACIÓN DEL CAPITAL DE TRABAJO
  - *IMP = gasto por impuesto a las ganancias; INTERESES = gastos financieros*
  - *Si la empresa es europea, añade también "- ARRENDAMIENTOS"*
- **Conversión de Caja** = (FCFE + Intereses) / Beneficio Neto
- *Rango saludable: 70% - 90%*

---

## Faltas Eliminatorias Automáticas

Si se superan estos límites, la empresa puede quedar descartada directamente:

| Falta Eliminatoria | Umbral |
|-------------------|--------|
| Deuda Neta / EBITDA | > 4x |
| ROE | < 15% (excepto financieras o situaciones muy justificadas) |
| Solvencia | < 20% |
| Conversión de Caja | Persistentemente < 50% |
| Sospechas de manipulación contable o deterioro extremo del margen | Cualquier evidencia |

---

## Estructura del Análisis

### FASE 0: FILTRO CERO

- Describe brevemente el modelo de negocio y cómo genera dinero.
- Identifica los KPIs clave (ej. tiendas, usuarios, etc.).
- ¿Hay razones obvias para el descarte inmediato (fraude, complejidad excesiva)?

### FASE 1: EXAMEN CUANTITATIVO

Aplica las fórmulas exactas recogidas en el bloque superior:

#### Bloque 1: P&L (15%)
- Analisa la evolución de ventas y márgenes (Bruto, EBIT, Neto) de todo el periodo contenido en los archivos adjuntos.
- Calcula la CAGR de los ingresos y de los distintos márgenes a lo largo del periodo completo.
- Presenta una tabla con los datos anuales y el CAGR resultante.

#### Bloque 2: Estimaciones (15%)
- Busca el consenso de analistas y crecimiento esperado del BPA a 3-5 años.

#### Bloque 3: Valoración Histórica (15%)
- Calcula PER actual y EV/EBIT (Capitalización + Deuda Neta / EBIT).

#### Bloque 4: Calidad y Crecimiento (25%) — BLOQUE PRIORITARIO
- Calcula ROE (>15%), ROCE y Tasa de Reinversión según las fórmulas indicadas.

#### Bloque 5: Salud Financiera (15%)
- Calcula Deuda Neta/EBITDA (<2.5x), Solvencia (>35%), y el Ciclo de Conversión de Efectivo (CCC).
- Aplica el método de promedios indicado y advierte si faltan datos.

#### Bloque 6: Generación de Caja (15%)
- Calcula el FCFE con la fórmula exacta (usando EBIT como base y, si es empresa europea, restando arrendamientos).
- Calcula la Conversión de Caja. Una conversión sana se sitúa entre el 70% y el 90%.

---

## Sistema de Puntuación Final

- Asigna una nota del 1 al 10 según la ponderación de la guía.
- **Faltas Eliminatorias:** Indica explícitamente si la empresa incurre en alguna falta según los umbrales automáticos listados.
- **Conclusión:** ¿Merece un análisis profundo según la nota de corte de 8/10?

---

## Consejos de Uso

1. **Archivos necesarios:** Informes 10-K o anuales de la empresa (PDF o DOCX). Extraer capítulos 1, 7 y 8.
2. **Datos de mercado:** Capitalización de mercado, precio por acción, BPA (obtenibles vía web search).
3. **Si faltan datos:** Indicar explícitamente como limitación antes de omitir un cálculo.
4. **Verificación cruzada:** Siempre confirmar escala (miles vs millones) y año correcto antes de calcular.
