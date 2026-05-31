## 👤 Mi información 

- **Nombre:** Julio Reynaldo Pellecer Morales 
- **Carné:** 241071
- **Universidad:** Universidad del Valle de Guatemala
- **Curso:** Sistemas y Tecnologías Web 2026

# 🎮 Mi Backlog Personal

Aplicación full-stack para gestionar tu colección personal de videojuegos. Permite registrar juegos, cambiar su estado (pendiente, jugando, completado, abandonado), visualizar estadísticas y persistir datos tanto en LocalStorage como en una base de datos remota.



### 📊 Mi gráfica original — Juegos por estado

La gráfica de distribución por estado muestra cuántos juegos tengo en cada etapa 
disponible de mi backlog (pendiente, jugando, completado, abandonado). La elegí porque me
parece que es la información más útil para un backlog personal. Con ella puedo ver si tengo 
demasiados juegos abandonados o si estoy jugando varios a la vez. Cada barra tiene 
su propio color para distinguir cada estado sin necesidad de leer las etiquetas.

### ⚙️ Mis 3 decisiones técnicas

**(1) Estructura del reducer**

Organicé las acciones en dos grupos: las que modifican la lista de juegos 
(HIDRATAR, AGREGAR, ELIMINAR, CAMBIAR_ESTADO, REGISTRAR_ACTIVIDAD) y las que 
modifican los filtros (FILTRAR, LIMPIAR_FILTROS). Esta separación hace que el 
reducer sea más fácil de leer y mantener, ya que cada grupo tiene una 
responsabilidades espicificas asingnadas, evitando problemas en la lógica. 

**(2) Acción más difícil — REGISTRAR_ACTIVIDAD**

Fue la más compleja porque requería actualizar un campo anidado dentro de 
`atributos.horasTotales` sin mutar el estado anterior. La solución fue usar 
spreading en dos fases: primero copiar el item completo con ...item, y 
luego copiar los atributos con ...item.atributos cambiando solo horasTotale`. 

**(3) Gráfica más compleja — Actividad últimos 7 días**

Esta gráfica fue la más difícil porque requería transformar datos. Generar 
un array de los últimos 7 días , calcular cada fecha con, y 
luego comparar esas fechas con la propiedad fechaRegistro de 
cada juego para contar cuántos fueron agregados cada día. Todo esto se realiza
dentro de un useMemo para que no se recalcule en cada render.


### 🔍 Análisis del Profiler — useMemo

#### ANTES de useMemo
<img width="451" height="723" alt="image" src="https://github.com/user-attachments/assets/9ea00519-b45f-47d3-a0f6-a2fc892430bf" />

Sin useMemo, cada letra escrita en el buscador provocaba que todos los 
componentes se recargen incluyendo JuegoCard para cada juego, 
aunque ninguno haya cambiado. Esto se debe a que la función de filtrado 
se ejecutaba en cada render y producía un array nuevo, lo que React 
interpretaba como un cambio de props.

#### DESPUÉS de useMemo
<img width="1765" height="1071" alt="Captura de pantalla 2026-05-30 162552" src="https://github.com/user-attachments/assets/1dc841c1-e682-414e-89fe-4230264cf611" />


Con useMemo, la lista filtrada solo se recalcula cuando cambian lista, 
filtroCategoria, filtroEstado o busqueda. Los componentes JuegoCard 
envueltos en React.memo dejaron de re-renderizarse al escribir en el 
buscador si el juego no estaba siendo filtrado, reduciendo significativamente 
el trabajo del navegador.

## 🔗 URLs

- 🌐 Aplicación Web Pública| [proyecto-final-sistemas-y-tecnolog.vercel.app](https://proyecto-final-sistemas-y-tecnolog.vercel.app)
  
- ⚙️ Backend API | [backlog-personal-backend.onrender.com](https://backlog-personal-backend.onrender.com)
  
- 📦 Repositorio | [GitHub](https://github.com/Guate27/Proyecto-Final-Sistemas-y-Tecnolog-as-Web-) |


## 📸 Screenshots

<img width="1918" height="1066" alt="Captura de pantalla 2026-05-31 141858" src="https://github.com/user-attachments/assets/d8ac405a-6936-457c-9245-c61220d66369" />

<img width="1911" height="1060" alt="Captura de pantalla 2026-05-31 141759" src="https://github.com/user-attachments/assets/bedc6f17-e82d-4f5a-b934-531e125b3926" />


<img width="1919" height="1149" alt="Captura de pantalla 2026-05-31 142028" src="https://github.com/user-attachments/assets/d0113db3-8c15-44cc-8987-697f6f4dca78" />

<img width="1916" height="1069" alt="Captura de pantalla 2026-05-31 142050" src="https://github.com/user-attachments/assets/51289fdf-1efa-45ff-8ac1-f97d3e590d75" />


## 🛠️ Stack tecnológico

### Frontend
- React: Librería UI |
- Vite: Servidor de desarrollo frontend
- Recharts: Visualizador de gráficas |
- JavaScript: Lenguaje de programción para desarrollo de servicios web 
- Variables CSS: Paleta de colores del sistema

### Backend
- Node.js: Entorno local de ejecución para código JavaScript
- Express:  Librearía para el desarrollo de servidore
- better-sqlite3: Base de datos Local
-  dotenv: Variables de entorno

### Deploy
- Vercel: Hosting del frontend
- Render: Hosting del backend
- GitHub: Control de versiones 

---

## 🚀¿Cómo probar la aplicaicón?

### Requisitos previos
- Node.js 18 o superior
- npm 9 o superior
- Git
### Instrucciones generales
Por cada acción listada a continuación ejecutar los comandos correspondientes en una terminal tipo cammand prompt distinta para cada acción. 

### Clonar el repositorio
1. git clone https://github.com/Guate27/Proyecto-Final-Sistemas-y-Tecnolog-as-Web-.git

### Levantar el backend
1. cd Proyecto-Final-Sistemas-y-Tecnolog-as-Web-
2. cd backend
3. npm install
4. node src/index.js
5. Acceder al backend ejecutado: `http://localhost:3001`

### Levantar el frontend
1. cd Proyecto-Final-Sistemas-y-Tecnolog-as-Web-
2. cd frontend
3. npm install
4. npm run dev
5. Acceder al frotend ejecutado: `http://localhost:5173`

### 4. (Opcional) Configurar variable de entorno del frontend
Crear un archivo `frontend/.env` con:
VITE_API_URL=http://localhost:3001


## 🎮 Mis primeros Items (Fase 1)

Durante la Fase 1, agregué el siguiente videojuego al sistema para validar el flujo completo del CRUD:

| Nombre | Categoría | Estado | Plataforma |
|--------|-----------|--------|------------|
| The Witcher | RPG | Pendiente | PC |

Este item permitió verificar que el flujo de creación, lectura, edición y eliminación funcionara correctamente tanto en LocalStorage como en la API.


## 🎨 Mi paleta de colores

### Tema claro
- | `--color-fondo` | `#f7f7f8` | Tonalidad de gris para la base o fondo  
- | `--color-superficie` | `#f0f0f2` | Un poco más oscuro que el fondo para distinguir tarjetas y formularios 
- | `--color-texto` | `#1a1a1a` | Negro para que sea más fácil de distinguir la informaión 
- | `--color-texto-secundario` | `#6b7280` | Gris para información secundaria   
- | `--color-acento` | `#4f46e5` | Morado
- | `--color-borde` | `#e5e7eb` | Gris para definir los límites del contenido 

### Tema oscuro
- | `--color-fondo` | `#0f172a` | Azul muy oscuro como base 
- | `--color-superficie` | `#1e293b` | Azul oscuro más claro que el fondo 
- | `--color-texto` | `#f1f5f9` | Blanco para facilitar la lectura del contenido 
- | `--color-texto-secundario` | `#94a3b8` | Gris azulado para información secundaria  
- | `--color-acento` | `#818cf8` | Morado claro para que el contenido sea fácil de ver en fondos oscuros
- | `--color-borde` | `#334155` | Azul oscuro para definir los límites de contenido
