---
name: analisis-inversion-accion
description: Use this skill when the user asks to evaluate a stock or company for investment (comprar, invertir, evaluar, analizar empresa/acción/ticker). It provides a fixed research workflow using GuruFocus data and formats the report like the AVGO analysis, including a polished PDF in the current folder.
---

# Skill: Análisis integral de inversión de acciones (GuruFocus)

## Cuándo usarla
Activa cuando el usuario pida:
- evaluar, analizar o decidir si invertir en una empresa/acción/ticker
- revisar fundamentals, valuación, riesgos, dividendos, insider/guru activity
- generar pdf de análisis de inversión

## Entradas esperadas
- Ticker/símbolo y mercado (ej. NASDAQ:AVGO).
- API key de GuruFocus (si aplica). No almacenar en archivos; úsala solo en memoria/sesión.

## Flujo obligatorio
1. Obtener datos con GuruFocus (auth requerido):
   - stock profile
   - stock rankings
   - stock fundamentals
   - stock valuations
   - stock segments
   - stock dividends (si no está completo en profile)
   - stock news (1-2 páginas)
   - stock insider trades
   - stock guru holdings/trades (si disponible)
2. Calcular y presentar (si faltan) por acción y totales:
   - Revenue, márgenes, utilidad, FCF; crecimiento 1/3/5/10 años; trimestres recientes.
   - Balance, deuda, caja, D/E, D/EBITDA, interest coverage, liquidez, goodwill/tangible book, Z/F-score.
   - Valuación: P/E, P/E forward, P/S, P/B, P/FCF, EV/EBITDA, FCF yield, dividend yield; GF Score y ranks; GF Value vs DCF; rangos históricos.
   - Capital allocation: payout, buybacks, R&D, M&A, dividend growth.
   - Señales: insider buys/sells, guru positions/trades, sentiment cuantitativo.
3. Estructurar el reporte con estas secciones (en español):
   1. Resumen ejecutivo (veredicto corto, calidad, atractivo, riesgos)
   2. Negocio y posicionamiento (mix de ingresos, geografía)
   3. Desempeño financiero y crecimiento (tablas anuales + trimestrales)
   4. Rentabilidad, balance y riesgo financiero
   5. Capital allocation y dividendos
   6. Valuación (múltiplos actuales, GF, DCF, histórico, analistas)
   7. Señales de mercado, insiders y gurus
   8. Riesgos clave
   9. Fortalezas competitivas (moat)
   10. Respuesta a la pregunta (escenarios + parámetros prácticos + alertas)
   11. Cierre y disclaimer
4. Mantener formato profesional, tablas bien alineadas y cifras con unidades.
5. Incluir disclaimer: informativo, no asesoría de inversión; fuentes y fecha.

## Reglas de salida
- Reporte principal en Markdown en el chat.
- Si se solicita PDF:
  - Generar HTML con el mismo contenido y CSS limpio (títulos, tablas, callouts).
  - Convertir a PDF con `libreoffice --headless --convert-to pdf --outdir <carpeta_actual> <archivo>.html`.
  - Nombre: `analisis_<TICKER>.pdf` (ej. `analisis_AVGO.pdf`).
  - Verificar que el PDF existe y reportar tamaño/ruta.
- No guardar API keys en archivos/repositorio.
- Si faltan datos o fallan endpoints, indicarlos claramente y continuar con fuentes disponibles.

## Plantilla de veredicto (ajustar)
- Calidad de negocio: excelente/muy buena/buena.
- Atractivo actual: oportunidad razonable / justa / cara.
- Perfil apto: growth largo plazo vs conservador/income vs trading.
- Entrada: escalonada (DCA), sizing moderado (p.ej. 2-5% portafolio growth), checkpoints trimestrales, alertas de reducción.

## Red/Green flags (siempre incluir)
- Red: leverage goodwill/tangible negativo, M-score, insider/guru venta, customer concentration, valuación absoluta.
- Green: márgenes/FCF, crecimiento, D/EBITDA, GF Score, GF Value, quality ranks.

## Archivos de salida esperados (carpeta actual)
- `analisis_<TICKER>.html`
- `analisis_<TICKER>.pdf`
