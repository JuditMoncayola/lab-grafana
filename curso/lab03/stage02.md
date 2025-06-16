## 🧩 Fase 2 – Navegabilidad entre paneles y preparación de filtros

---

### 🎯 Objetivo

Habilitar navegación desde los nodos del panel SCADA hacia dashboards de detalle, pasando variables para contextualizar la vista. Introducir la lógica de filtros simples basados en CSV.

---

### 🗂️ Scaffolding

* Dashboard actual: `dashboard-overview`
* Nuevo dashboard: `detalle-camara`
* Variables: `camara` (tipo `custom`)
* CSV de ejemplo montado en Codespaces: `/data/camaras.csv`

---

### 🪜 Pasos guiados

1. **Crear la variable `camara` en dashboard-overview**

   * ⚙️ (Dashboard settings) → Variables → `New`

     * **Name:** `camara`
     * **Type:** `Custom`
     * **Values:** `Vacuno,Porcino,Ovino`
     * **Include All Option:** ✅

2. **Actualizar los nodos para navegar a detalle**

   * Edita el Mermaid y añade enlaces con `click`:

     ```mermaid
     click Cámara_1 "d/detalle-camara?var-camara=Vacuno" "Ver detalle Vacuno"
     click Cámara_2 "d/detalle-camara?var-camara=Porcino" "Ver detalle Porcino"
     click Cámara_3 "d/detalle-camara?var-camara=Ovino" "Ver detalle Ovino"
     ```

3. **Crear el dashboard `detalle-camara`**

   * Nuevo dashboard → Añadir panel vacío → Guardar como `detalle-camara`

4. **Agregar variable `camara` también en `detalle-camara`**

   * Mismo nombre: `camara`
   * Tipo: `Custom` o `Query` si quieres alimentar desde CSV en pasos futuros

5. **Probar la navegación**

   * Desde el panel principal, haz clic en cada cámara → debe abrir el `detalle-camara` con la variable `camara` aplicada.

6. **(Opcional)** Mostrar la variable activa

   * En un panel de texto o título, usa `$camara` para mostrar la cámara seleccionada.

---

### 🎯 Retos

1. 🔗 **Haz que los nodos individuales (ej: 🚨 Alarma) también naveguen al detalle**

   * *Tip:* Puedes usar `click A1 "..."` directamente sobre el nodo, no solo sobre el subgraph.

2. 🧪 **Simula que una de las cámaras dispara una alarma (nodo en rojo) y navega a su detalle**

   * *Tip:* Usa el estilo `fill:#f1948a` para la alarma y prueba si cambia el foco del usuario.

3. 📥 **Haz que el CSV de cámaras alimente dinámicamente los valores de la variable `camara`**

   * *Tip:* Si usas el plugin CSV como Data Source, en la variable `Query` selecciona la columna `camara` única con `distinct`.

---

### ✅ Validaciones

* Al hacer clic en una cámara, el dashboard de detalle se abre con la variable correcta.
* La URL refleja `?var-camara=...`
* La variable `camara` está presente y usable en ambos dashboards.

---

### 💬 Reflexión

Este paso representa el **paso de contexto** entre vista general y vista concreta, como en los SCADAs industriales. Aunque los datos aún no se visualizan, el marco de navegación está preparado para alimentar KPIs, indicadores o alertas específicas.