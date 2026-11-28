# ONLIMED — Marketplace de Servicios Médicos (MVP Posadas, Misiones)

**Onlimed** es una plataforma digital de intermediación que conecta pacientes con médicos y profesionales de la salud independientes en la ciudad de Posadas, Misiones, Argentina.

> **Aviso Importante:** Onlimed no es una clínica ni presta servicios médicos directos. No almacena historias clínicas, diagnósticos ni gestiona emergencias médicas. En caso de urgencia sanitaria, comunicarse a la línea oficial **107 (Emergencias Médicas)**.

---

## 🚀 Arquitectura y Tecnologías Utilizadas

- **Framework:** [Next.js](https://nextjs.org/) (App Router, Server Components y Client Components optimizados).
- **Lenguaje:** TypeScript estricto con tipado completo de entidades de salud.
- **Estilos:** Tailwind CSS con una paleta moderna, limpia y minimalista (azul médico `#0284C7`, verde menta `#0D9488`, slate suave `#F8FAFC`).
- **Iconos:** Lucide Icons.
- **Base de Datos & Auth:** Supabase (PostgreSQL) con políticas de seguridad por fila (**Row Level Security - RLS**), combinado con un **Store reactivo híbrido** con persistencia en navegador para testing y demo inmediata.

---

## 📦 Módulos del Sistema

El producto se compone de tres módulos funcionales integrados:

### 1. Marketplace Público (`/`, `/profesionales`, `/profesionales/[id]`)
- **Buscador en Hero:** Búsqueda en tiempo real por nombre de médico, especialidad o servicio médico.
- **Filtros por Barrios de Posadas:** Centro, Villa Sarita, Palomar, Villa Cabello, Itaembé Miní, Costanera.
- **Filtros por Disponibilidad y Matrícula Verificada.**
- **Ficha del Profesional:** Biografía, matrícula, formación médica, ubicación de consultorios y honorarios orientativos.
- **Flujo de Solicitud de Turnos en 5 pasos:**
  1. Selección de servicio
  2. Selección de fecha de atención
  3. Selección de horario libre (con prevención de solapamientos)
  4. Datos mínimos de contacto (sin registro previo obligatorio)
  5. Confirmación con código de seguimiento (`ONL-XXXX`) y estado **Pendiente**.

### 2. Panel Privado del Profesional (`/panel-medico`)
- **Dashboard de Métricas:** Solicitudes nuevas, turnos confirmados, cancelados y total de pacientes.
- **Gestión de Turnos:** Confirmar solicitudes, rechazar con motivo o cancelar, con enlace directo para contactar al paciente por WhatsApp o llamada.
- **Agenda y Disponibilidad:** Configuración de días de atención, horarios de inicio y fin, y bloqueo de franjas horarias.
- **Edición de Perfil:** Modificación en vivo de biografía, especialidad, consultorios en Posadas y servicios con honorarios.
- **Selector de Médico Demo:** Permite alternar fácilmente entre los perfiles cargados (Dr. Martín Alvarenga, Dra. Sofía Valenzuela, etc.) para probar el panel.

### 3. Panel de Administración Onlimed (`/admin`)
- **Validación Manual de Matrículas:** Cumplimiento estricto de la regla: *ninguna matrícula se aprueba automáticamente*. Aprobación o rechazo con trazabilidad.
- **Gestor de Publicación:** Activar o pausar profesionales en el marketplace.
- **Administrador de Especialidades:** Alta, edición y baja de categorías médicas.
- **Auditoría de Turnos:** Visualización de todas las solicitudes y citas emitidas en la plataforma.
- **Asignación Manual de Planes:** Gratuito, Profesional y Premium.
- **Botón de Reset:** Restablecer el estado inicial de datos ficticios en cualquier momento.

---

## 🛠️ Instalación y Puesta en Marcha

### Prerrequisitos
- Node.js versión 18+ (recomendado 20 o 24).
- npm o pnpm.

### 1. Clonar e instalar dependencias
```bash
npm install
```

### 2. Configuración de Variables de Entorno (Opcional para Supabase)
El proyecto incluye un fallback reactivo que permite probar **el 100% de la funcionalidad de forma interactiva e inmediata sin credenciales**, guardando los cambios en el navegador.

Para conectar con tu instancia real de **Supabase**:
1. Copiar `.env.example` a `.env.local`:
   ```bash
   cp .env.example .env.local
   ```
2. Completar las variables con los datos de tu proyecto de Supabase:
   ```env
   NEXT_PUBLIC_SUPABASE_URL=https://tu-proyecto.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=tu-anon-key-aqui
   ```
3. Ejecutar las migraciones SQL en el SQL Editor de Supabase:
   - `supabase/schema.sql`: Creación de tablas, enums, índices y RLS.
   - `supabase/seed.sql`: Carga de datos de demostración en Posadas.

### 3. Iniciar el Servidor de Desarrollo
```bash
npm run dev
```
Abrir [http://localhost:3000](http://localhost:3000) en el navegador.

---

## 👤 Perfiles de Prueba y Roles (Datos Ficticios de Posadas)

| Rol | Profesional | Especialidad | Matrícula | Barrio en Posadas | Plan |
|---|---|---|---|---|---|
| **Médico (Cardiología)** | Dr. Martín Alvarenga | Cardiología | MP 4182 (Verificada) | Centro (Félix de Azara 1845) | Premium |
| **Médico (Pediatría)** | Dra. Sofía Valenzuela | Pediatría | MP 5291 (Verificada) | Villa Sarita (Alvear 1420) | Profesional |
| **Médico (Traumatología)**| Dr. Lucas Benítez | Traumatología | MP 3890 (Verificada) | Palomar (Av. Mitre 2180) | Profesional |
| **Médico (Dermatología)** | Dra. Camila Schmidt | Dermatología | MP 6124 (Pendiente) | Centro (San Martín 1540) | Gratuito |
| **Administrador** | Staff Onlimed | Auditoría / Gestión | N/A | Acceso en `/admin` | Admin |
| **Paciente** | Paciente General | Acceso libre sin login | N/A | Posadas y alrededores | N/A |

---

## ⚖️ Aspectos Legales y Privacidad (Privacy by Design)

- Páginas accesibles en el pie de página:
  - [Términos y Condiciones](/terminos): Regula la condición de intermediación tecnológica y delimita la responsabilidad del acto médico.
  - [Política de Privacidad](/privacidad): Cumple la Ley Nacional 25.326. No se recopilan diagnósticos ni historias clínicas.
