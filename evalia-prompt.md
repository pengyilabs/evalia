# METIS — AI Exam Generation Platform

Build a single-page AI-powered exam generation and test-taking platform in Spanish. The app has sidebar navigation, client-side routing, and multiple interactive pages. All UI copy is in Spanish.

## Design Tokens

- `--bg: #f8f9fb`
- `--surface: #ffffff`
- `--dark: #111111`
- `--green: #5CE63F`
- `--muted: #6b7280`
- `--border: #e5e7eb`
- Font: Inter (400–900)
- Border radius: 12px (cards), 8px (controls), 9999px (pills)
- Sidebar width: 240px
- Topbar height: 64px

## Layout

- Fixed left sidebar with logo, 3 nav items (Inicio, Materiales, Reportes), and a dark plan card at the bottom
- Topbar with breadcrumb title, credits counter, icon buttons, and avatar
- Pages show/hide via `showPage()` function with hash-based routing (`#dashboard`, `#materials`, `#reports`, `#create`, `#wizard`, `#editor`, `#fill-test`)
- Sidebar and topbar hide on full-screen pages (create, wizard, editor, fill-test)

## Pages

### 1. Dashboard (`page-dashboard`)

- **Welcome banner**: Green gradient background, greeting text ("Hola, [Name]"), subtitle ("¿Listo para crear tu próxima evaluación?"), and a "Crear evaluación" button
- **AI Idea banner**: Light green gradient, lightbulb icon, "Empezar desde cero" heading, "Usa IDEA para generar una evaluación completa desde tu material" subtitle, "Generar con IDEA" button
- **Recent evaluations section**: Header with "Evaluaciones recientes" title and "Ver todas" link. Grid of eval cards (min 300px each). Each card has: colored thumbnail area, title, description, metadata (date, questions, duration), and a 3-dot dropdown menu with share/edit/duplicate/delete actions
- **Quick actions section**: 3 cards in a row — "Subir material" (upload icon), "Generar desde IDEA" (sparkles icon), "Ver reportes" (chart icon)

### 2. Materials Page (`page-materials`)

- **Header**: "Materiales" title, subtitle, and "Subir material" button
- **Filter bar**: Search input, filter pills (Todos, PDF, PPT, DOC, CSV, TXT), and file count
- **Materials table**: Rows with checkbox, file type icon (color-coded: PDF=red, PPT=orange, DOC=blue, CSV=green, TXT=gray), filename, source, date, size, and action buttons (download, delete)
- **Upload modal**: Drag-and-drop zone with dashed border, file input, cancel and upload buttons

### 3. Create Page (`page-create`)

- Full-screen layout (no sidebar/topbar)
- **Left side**: Large illustration area with green gradient background
- **Right side**: "Crear nueva evaluación" heading, subject input, file upload area, experience level selector (Básico/Intermedio/Avanzado as pills), custom instructions textarea, and "Generar con IDEA" button
- **Attachment button**: Opens dropdown with two tabs — "Subir archivo" (file input) and "Plataforma educativa" (grid of platform options: Classroom, Moodle, Canvas, Blackboard, Teams, Google Drive)

### 4. Wizard (`page-wizard`)

- Full-screen with 4-step progress indicator at top
- **Step 1 — Processing materials**: Chat-style interface with typing indicators. Borderless textarea at bottom, attachment button, and "Procesar" button. Shows AI processing messages with sprite animations
- **Step 2 — Outline editor**: Draggable blocks, each containing:
  - Editable question text input
  - Clickable type badge that cycles through: ✓ Única (blue), ☑ Múltiple (yellow), ✎ Abierta (green)
  - Source citation with document icon
  - Editable option inputs (A/B/C/D for Única/Múltiple)
  - Move up/down and delete buttons
  - "Add block" button and question counter ("X preguntas en total")
- **Step 3 — Question configuration**
- **Step 4 — Review and generate**

### 5. Editor (`page-editor`)

- Dark-themed full-screen editor
- **Topbar**: Back button ("Volver"), title, and "Generar" button
- **Left sidebar**: Question list with numbered items, click to navigate
- **Main area**: Question cards showing question text, type badge, options list, correct answer toggle, and edit/delete actions
- **Right preview panel**: Live preview of how the question will appear to students

### 6. Share Modal

- Centered modal with backdrop
- Shareable link with copy button
- Social sharing buttons (WhatsApp, email)
- QR code preview
- "Iniciar prueba" button (navigates to fill-test)

### 7. Fill Test Page (`page-fill-test`)

- Full-screen with no sidebar
- **Intro modal**: Centered card with 300px avatar image, typewriter effect greeting ("¡Hola! Soy Metis, tu asistente de estudio..."), and "Empezar prueba" button
- **Test interface**:
  - Left: Question display with one question at a time, radio/checkbox options for multiple choice, textarea for open questions
  - Top: Progress bar, question counter (1/12), 25-minute countdown timer
  - Bottom: Previous/Next navigation buttons, dot indicators for each question
  - Right: Collapsible AI chat panel

### 8. AI Chat Panel (in fill-test)

- **Header**: Metis avatar (300px SVG sprite), name, status ("En línea")
- **Messages area**: AI messages with typing indicators (3 bouncing dots), user messages
- **Sprite system**: 83+ SVG emotion sprites mapped to contexts:
  - Greeting: waving, happy, peace-sign
  - Thinking: thinking, chin-rest, looking-up, focusing
  - Encouraging: thumbs-up, okay-sign, nodding, confident
  - Explaining: explaining-both-hands, pointing-up, presenting
  - Celebrating: celebrating, clapping, excited, proud
  - Listening: listening, headphones
  - Concerned: worried, nervous-smile, serious
  - Playful: giggling, heart-hands, mic-drop
  - Working: typing, writing, reading-notes
  - Neutral: neutral, shrugging, sipping-coffee
- **Sprite cycling**: During AI thinking, sprites cycle every 1.5 seconds through thinking variants
- **Message-based sprite switching**: Keywords in AI messages trigger appropriate sprite (e.g., "¡hola" → greeting, "excelente" → celebrating, "por qué" → explaining)
- **Mic button**: Pulsing green animation, starts simulated voice recording
- **Voice recording simulation**: Click mic → creates user chat bubble in messages area → types character-by-character at 35ms/char with blinking cursor → Cancel (X) removes bubble → Send (✓) sends as user message and triggers AI response
- **Chat input**: Text input with send button, Enter to send
- **Delayed greetings**: On question change, AI sends delayed greeting after 2 seconds with typing indicator

### 9. Reports Page (`page-reports`)

- **Summary cards row**: 4 cards — Evaluaciones (12), Estudiantes (345), Nota media (7.8), Tasa aprobación (82%)
- **Difficulty analysis**: Horizontal bars showing Difícil (35%), Media (45%), Fácil (20%)
- **AI prompt usage per question**: Table showing question number, prompt used, success rate
- **Test performance table**: Table with columns: Evaluación, Fecha, Estudiantes, Nota media, Tasa aprobación
- **Common mistakes section**: List of frequently missed questions
- **AI assistant usage stats**: Chat sessions, messages sent, avg response time

## Key Interactions

- `showPage(page)`: Shows/hides pages, updates sidebar active state, manages sidebar/topbar visibility
- Hash-based routing with `hashchange` listener
- `cycleQType(el)`: Cycles question type badge through Única → Múltiple → Abierta
- `addOutlineBlock()`: Adds new draggable question block with editable fields
- `removeBlock(btn)`: Removes block with fade animation
- `moveBlock(btn, dir)`: Reorders blocks up/down
- `renumberBlocks()`: Updates question numbers and counter
- `toggleFillMic()`: Starts/stops voice recording simulation
- `startSimulatedRec()`: Creates user bubble, types text character-by-character
- `cancelFillRec()`: Removes recording bubble
- `sendFillRec()`: Sends recorded message, triggers AI response
- `sendFillChat()`: Sends user message from text input
- `startSpriteCycle()`: Cycles through thinking sprites every 1.5s
- `stopSpriteCycle()`: Stops sprite cycling
- `setSpriteForMessage(text)`: Sets appropriate sprite based on message keywords
- `addFillTyping(container, cb)`: Shows typing indicator, removes after 1.5s
- `addFillAiMsg(container, text, delay)`: Adds AI message with fade-in animation
- `startFillTimer()`: 25-minute countdown with MM:SS display
- `filterMaterials()`: Filters material list by search query and type pill
- `handleFileUpload()`: Processes file selection
- `toggleAttachMenu()`: Shows/hides attachment dropdown
- `toggleEvalDropdown(btn)`: Shows/hides eval card dropdown menu

## Technical Notes

- Single self-contained HTML file
- All SVG sprites referenced from `evalia-sprites/` folder
- Google Fonts loaded for Inter
- Client-side routing only (no server)
- No external JS frameworks — vanilla JavaScript
- CSS transitions for all state changes (fade, slide, scale)
